
## Step 1: Prepare the Ubuntu Cloud-init Image

#### [](https://dev.to/minerninja/create-an-ubuntu-cloud-init-template-on-proxmox-the-command-line-guide-5b61#11-download-the-ubuntu-cloud-ima1.1 Download the Ubuntu Cloud Image:
```bash
qm importdisk 501 /var/lib/vz/template/iso/ubuntu-24.04-server-cloudimg-amd64.img local-lvm
```

```
```