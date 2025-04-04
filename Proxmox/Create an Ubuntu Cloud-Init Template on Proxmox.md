
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

### 2.1. Create a new Virtual Machine (VM):

Create a VM with a unique identifier `501` (or any other available ID):

```bash
qm create 9000 --name "ubuntu-cloud-init-template" --memory 2048 --cores 2 --net0 virtio,bridge=vmbr0
```
- `9000` — Unique identifier for the VM.
- `--name` — Name of the virtual machine.
- `--memory` — Amount of RAM in megabytes.
- `--cores` — Number of CPU cores.
- `--net0` — Network card configuration (uses `virtio` with bridge `vmbr0`).

#### [](https://dev.to/minerninja/create-an-ubuntu-cloud-init-template-on-proxmox-the-command-line-guide-5b61#23-import-the-downloaded-image-into-the-proxmox-storage)2.3 Import the downloaded image into the Proxmox storage

Use `qm importdisk` to import the downloaded image into local storage:
```bash
qm importdisk 501 /var/lib/vz/template/iso/ubuntu-24.04-server-cloudimg-amd64.img local-lvm
```

```
```