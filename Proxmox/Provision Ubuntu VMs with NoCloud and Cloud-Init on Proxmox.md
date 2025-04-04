Creating repeatable and secure VM templates in your Proxmox environment is a game-changer for homelabbers and sysadmins alike. 

In this post, you'll learn how to:

- Use the NoCloud datasource with Ubuntu Cloud Images

- Inject SSH keys from your Mac or admin box

- Enable and verify the Proxmox guest agent

- Clone pre-configured VMs using Proxmox CLI


Let’s walk through the whole process—from image preparation to SSH-ready VM deployment.
For the latest Ubuntu Cloud images, you can check [Ubuntu Cloud Images](https://cloud-images.ubuntu.com/).

## Step 1: Download the Ubuntu Cloud Image

From your **Proxmox server**, download the latest Ubuntu 24.04 cloud image:

```bash
wget -P /var/lib/vz/template/iso/ https://cloud-images.ubuntu.com/daily/server/releases/24.04/release/ubuntu-24.04-server-cloudimg-amd64.img
```

Then verify:

```bash
ls /var/lib/vz/template/iso/
```

You should see the `.img` file listed.

## Step 2: Create a Base VM Template

### 2.1 Create the VM

```bash
qm create 501 \
  --name ubuntu-cloud-init-template \
  --memory 2048 \
  --cores 2 \
  --net0 virtio,bridge=vmbr0
```

### 2.2 Import the disk

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

## Step 3: Create Your NoCloud ISO

I'll generate the `nocloud.iso` from my **Mac**, but any admin workstation will do.

### 3.1 Generate a dedicated SSH key

```bash
ssh-keygen -t ed25519 -C "ubuntu-template" -f ~/.ssh/id_ed25519_ubuntu_template
```

This creates:

- `~/.ssh/id_ed25519_ubuntu_template`

- `~/.ssh/id_ed25519_ubuntu_template.pub`

### 3.2 Create `user-data` (cloud-init)



### 1.2 Verify that the file was downloaded successfully

Make sure the file is in the correct directory:

```bash
ls /var/lib/vz/template/iso/
```
You should see `ubuntu-24.04-server-cloudimg-amd64.img` listed in the directory.

## Step 2: Create a Virtual Machine Template in Proxmox

### 2.1. Create a new Virtual Machine (VM)

Create a VM with a unique identifier `501` (or any other available ID):

```bash
qm create 501 --name "ubuntu-cloud-init-template" --memory 2048 --cores 2 --net0 virtio,bridge=vmbr0
```
- `501` — Unique identifier for the VM.
- `--name` — Name of the virtual machine.
- `--memory` — Amount of RAM in megabytes.
- `--cores` — Number of CPU cores.
- `--net0` — Network card configuration (uses `virtio` with bridge `vmbr0`).

### 2.3 Import the downloaded image into the Proxmox storage

Use `qm importdisk` to import the downloaded image into local storage:

```bash
qm importdisk 501 /var/lib/vz/template/iso/ubuntu-24.04-server-cloudimg-amd64.img local-zfs
```
- `501` — ID of the virtual machine.
- Path to the Ubuntu Cloud-init image file.
- `local-zfs` — Name of the storage in Proxmox.

### 2.4 Configure the primary disk and VM settings

Set up the disk using the `scsi` type and configure the boot options:

```bash
qm set 501 --scsihw virtio-scsi-pci --scsi0 local-zfs:vm-501-disk-0
qm set 501 --boot c --bootdisk scsi0
```
- `--scsihw` — Specifies the SCSI controller type (using `virtio-scsi-pci`).
- `--scsi0` — Configures the primary disk of the VM.
- `--boot c --bootdisk scsi0` — Sets the VM to boot from the primary disk.

### 2.5. Add a Cloud-init disk

Add a Cloud-init disk to the VM:

```bash
qm set 501 --ide2 local-zfs:cloudinit
```
- `--ide2` — Specifies that the disk will be attached as an IDE device.
- `local-zfs:cloudinit` — Specifies the storage and type of the disk.

## Step 3: Configure Cloud-init

### 3.1 Generate a dedicated key for your Proxmox Ubuntu template

On your admin machine, run the following:
```bash
ssh-keygen -t ed25519 -C "ubuntu-template" -f ~/.ssh/id_ed25519_ubuntu_template
```
This will generate:

- `~/.ssh/id_ed25519_pve_template` (private)    
- `~/.ssh/id_ed25519_ubuntu_template.pub` (public)

### 3.2 Verify the key exists

```bash
ls ~/.ssh/id_ed25519_ubuntu_template*
```
You should see both the .pub and private key files.

### 3.3 Copy the **public key** to your Proxmox server

```bash
pbcopy < ~/.ssh/id_ed25519_ubuntu_template.pub
```

### 3.4 Once SSH’d into your Proxmox server

Run the `qm set` command to inject the SSH key into the Cloud-init-enabled VM template:

```bash
qm set 501 --sshkey 'Your_pasted_key_here...'
```
- Replace `501` with your template `VM ID`

Configure Cloud-init settings such as user, password, and SSH key:

```bash
qm set 501 --ipconfig0 ip=dhcp
qm set 501 --ciuser ubuntu --cipassword 'yourpassword'
qm set 501 --sshkey "$(cat ~/.ssh/id_rsa.pub)"
```
- `--ipconfig0 ip=dhcp` — Configures the IP to be assigned via DHCP.
- `--ciuser` — Specifies the Cloud-init username.
- `--cipassword` — Sets the password for the user (replace `'yourpassword'` with your desired password).
- `--sshkey` — Adds an SSH key for the user (the contents of the public key from `~/.ssh/id_rsa.pub`).

## Step 4: Save the Template

Convert the VM to a template:

```bash
qm template 501
```

## Step 5: Use the Template to Create New Virtual Machines

### 5.1 Clone the template to create a new VM

Create a new VM from the template:

```bash
qm clone 501 105 --name "new-ubuntu-vm"
```
- `105` — Unique ID for the new VM.
- `--name` — Name of the new virtual machine.

### 5.2 Configure the new VM

You can modify settings for the new VM, such as memory size and the number of cores:

```bash
qm set 105 --memory 4096 --cores 4
```

### 5.3 Start the new VM

```bash
qm start 105
```