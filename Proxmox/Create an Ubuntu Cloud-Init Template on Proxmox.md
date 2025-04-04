For the latest Ubuntu Cloud images, you can check [Ubuntu Cloud Images](https://cloud-images.ubuntu.com/).
## Step 1: Prepare the Ubuntu Cloud-init Image

### 1.1 Download the Ubuntu Cloud Image

To download the Ubuntu 24.04 image, use `wget` with the appropriate URL and save it to the `/var/lib/vz/template/iso/` directory:

```bash
wget -P /var/lib/vz/template/iso/ https://cloud-images.ubuntu.com/daily/server/releases/24.04/release/ubuntu-24.04-server-cloudimg-amd64.img
```
- `-P` — option tells wget to save the file in the specified directory

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
qm create 9000 --name "ubuntu-cloud-init-template" --memory 2048 --cores 2 --net0 virtio,bridge=vmbr0
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