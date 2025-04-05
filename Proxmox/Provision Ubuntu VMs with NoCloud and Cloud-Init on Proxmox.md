I’ve found that creating repeatable and secure VM templates in Proxmox is a game-changer—whether I’m working in a client environment or refining my homelab setup.

In this post, I’ll show you how to:

- Use the NoCloud datasource with Ubuntu Cloud Images

- Inject SSH keys from your admin box

- Enable and verify the Proxmox guest agent

- Clone pre-configured VMs using Proxmox CLI


Let’s walk through the whole process—from image preparation to SSH-ready VM deployment.
For the latest Ubuntu Cloud images, you can check [Ubuntu Cloud Images](https://cloud-images.ubuntu.com/).

## Step 1: Download the Ubuntu Cloud Image

From your **Proxmox server**, download the latest Ubuntu 24.04 cloud image:

```bash
wget -P /var/lib/vz/template/iso/ \
  https://cloud-images.ubuntu.com/daily/server/releases/24.04/release/ubuntu-24.04-server-cloudimg-amd64.img
```

Then verify:

```bash
ls /var/lib/vz/template/iso/ | grep -i ubuntu-
```

You should see the `ubuntu-24.04-server-cloudimg-amd64.img` file listed.

## Step 2: Create a Base VM Template

### 2.1 Create the VM

First, create the base VM that will serve as your Ubuntu template. We're using ID `501`, but you can choose any unused ID.

```bash
qm create 501 \
  --name ubuntu-cloud-init-template \
  --memory 2048 \
  --cores 2 \
  --net0 virtio,bridge=vmbr0
```

### 2.2 Import the disk

Next, import the Ubuntu cloud image as a virtual disk into your Proxmox storage (in this case, `local-zfs`).

```bash
qm importdisk 501 /var/lib/vz/template/iso/ubuntu-24.04-server-cloudimg-amd64.img local-zfs
```

### 2.3 Set the VM disk and boot options

```bash
qm set 501 \
  --scsihw virtio-scsi-pci \
  --scsi0 local-zfs:vm-501-disk-0 \
  --boot c \
  --bootdisk scsi0
```

### 2.4 Attach Cloud-init disk

```bash
qm set 501 --ide2 local-zfs:cloudinit
```

### 2.5 Enable the qemu-guest-agent

```bash
qm set 501 --agent enabled=1
```

## Step 3: Generate SSH Keys & NoCloud ISO

I'll generate the `ssh-keys` from my **Mac**, but any admin workstation will do.

### 3.1 Generate a dedicated SSH key

```bash
ssh-keygen -t ed25519 -C "ubuntu-template" -f ~/.ssh/id_ed25519_ubuntu_template
```

This creates:

- `~/.ssh/id_ed25519_ubuntu_template`

- `~/.ssh/id_ed25519_ubuntu_template.pub`

### 3.2 Copy the public key

```bash
pbcopy < ~/.ssh/id_ed25519_ubuntu_template.pub
```

### 3.3 Create `user-data` and `meta-data` (cloud-init)

SSH into your Proxmox server and navigate to a working directory.  
I’ll create the cloud-init configuration files that tell the VM how to initialize on first boot…

we’ll create the cloud-init configuration files that tell the VM how to initialize on first boot—things like hostname, users, and packages. The `user-data` file contains most of the logic, while `meta-data` just defines identity info for the instance.

```bash
mkdir -p /root/cloudinit/ubuntu-template
cd /root/cloudinit/ubuntu-template
```

 Create the following files:
`user-data`
```yml
#cloud-config
hostname: ubuntu-template
users:
  - name: ubuntu
    ssh-authorized-keys:
      - paste_the_public_key_you_copied_earlier
    sudo: ALL=(ALL) NOPASSWD:ALL
    shell: /bin/bash
package_update: true
package_upgrade: true
packages:
  - qemu-guest-agent
runcmd:
  - systemctl enable qemu-guest-agent
  - systemctl start qemu-guest-agent
```

`meta-data`
```yml
instance-id: ubuntu-template
local-hostname: ubuntu-template
```

### 3.4 Generate the ISO (on Proxmox)

Make sure you have `cloud-image-utils` installed:

```bash
apt update
apt install cloud-image-utils
```
> This gives you access to the `cloud-localds` command you need.

Then, generate the iso:

```bash
cloud-localds nocloud.iso user-data meta-data
```

### 3.5 Move ISO to `/var/lib/vz/template/iso/`

```bash
mv nocloud.iso /var/lib/vz/template/iso/
```
> If your Proxmox storage uses `local-lvm` instead of `local-zfs`, adjust the path accordingly.
> You can check available storage with: `pvesm status`

### 3.6 Attach ISO to VM

```bash
qm set 501 --ide2 local:iso/nocloud.iso,media=cdrom
```
> Replace `local` if your ISO storage is named differently — use `pvesm status` to check.

## Step 4: Convert to a Template

Once your base VM is configured, convert it to a Proxmox template so you can quickly clone new VMs from it.

```bash
qm template 501
```

## Step 5: Clone and Deploy

### 5.1 Clone the template

```bash
qm clone 501 105 --name "ubuntu-vm01"
```

### 5.2 Customize the new VM

```bash
qm set 105 --memory 4096 --cores 4
```

### 5.3 Start up the VM

```bash
qm start 105
```

![](attachments/Pasted%20image%2020250404205807.png)
> Remember to update the new IP address of the server in your `~/.ssh/config` file, as shown below.

`~/.ssh/config`

```
Host ubuntu
  HostName 10.160.0.64
  User ubuntu
  IdentityFile ~/.ssh/id_ed25519_ubuntu_template
```

Now you can type `ssh ubuntu` to connect to your newly created VM.

![](attachments/Pasted%20image%2020250404210159.png)

Nou now have a clean, reusable Ubuntu VM template that’s:

- Ready for hands-off, repeatable provisioning

- Fully compatible with cloud-init

- Pre-configured with the Proxmox guest agent

_Found this helpful?_ Check out more tech tutorials or follow my [GitHub](https://github.com/kfuras) where I share homelab setups, automation tools, and real-world projects from my work as an IT consultant.