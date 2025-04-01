- [[#Upgrade boot drive from single (RAID 0 ZFS) to dual RAID 1 and have both be bootable]]
- [[#Proxmox VE AdministrationGuide]]
- [[#Enable IOMMU on Proxmox running on uefi zfs raid1]]
- [[#Setup Postfix to Send Notifications (Email) Externally]]
- [[#Gmail for example:]]
- [[#Check SMART status for Disks]]
- [[#ZFS Alerts]]
- [[#If you are running a Proxmox host on a spare laptop]]
- [[#Here is a solution to hibernate all VMs at reboot or shutdown]]
- [[#Disable ‘No valid subscription’ notice on Proxmox]]

## Upgrade boot drive from single (RAID 0 ZFS) to dual RAID 1 and have both be bootable

> [!info] Can I upgrade my boot drive (RAID 0 ZFS) to RAID 1 _and_ have both be bootable?  
>  
> [https://www.reddit.com/r/Proxmox/comments/hjg5zh/comment/fwm29kh/?context=3](https://www.reddit.com/r/Proxmox/comments/hjg5zh/comment/fwm29kh/?context=3)  

## Proxmox VE Administration  
Guide  

> [!info] Proxmox VE Administration Guide  
> Proxmox VE is a platform to run virtual machines and containers.  
> [https://pve.proxmox.com/pve-docs/pve-admin-guide.html](https://pve.proxmox.com/pve-docs/pve-admin-guide.html)  

## Enable IOMMU on Proxmox running on uefi zfs raid1

**Systemd-boot**

1. Run `nano /etc/kernel/cmdline` and add the following at the end `intel_iommu=on iommu=pt`
2. Apply your changes by running `proxmox-boot-tool refresh`, which sets it as the option line for all config files in loader/entries/proxmox-*.conf.
3. Run `nano /etc/modules` and add the following lines:

```Shell
vfiovfio_iommu_type1vfio_pcivfio_virqfd
```

1. After changing anything modules related, you need to refresh  
    your initramfs. On Proxmox VE this can be done by executing:  
      
    `update-initramfs -u -k all`. Reboot to bring the changes  
    into effect and check that it is indeed enabled.  
    

## Setup Postfix to Send Notifications (Email) Externally

> [!info] [TUTORIAL] - Get Postfix to Send Notifications (Email) Externally  
> I'm not sure I did this in the proxmox way but I couldn't get email to relay to me and some posts were dated or didn't work for me, so I did the following: Gmail for example: Change.  
> [https://forum.proxmox.com/threads/get-postfix-to-send-notifications-email-externally.59940/](https://forum.proxmox.com/threads/get-postfix-to-send-notifications-email-externally.59940/)  

## **Gmail for example:**

Install package for passwd support:

```Plain
apt install libsasl2-modules
```

Install package for header change support:

```Plain
apt install postfix-pcre
```

Run `nano /etc/postfix/smtp_header_checks` and paste the following line:

```Plain
/^From:.*/ REPLACE From: hostname-alert hostname-alert@geekhaven.home
```

Run:

```Plain
postmap hash:/etc/postfix/smtp_header_checks
```

Run `nano /etc/postfix/main.cf` to include/change these lines:

```Plain
# New Gmail configuration
relayhost = [smtp.gmail.com]:587
smtp_use_tls = yes
smtp_sasl_auth_enable = yes
smtp_sasl_security_options = noanonymous
smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd
smtp_tls_CAfile = /etc/ssl/certs/ca-certificates.crt
smtp_header_checks = pcre:/etc/postfix/smtp_header_checks

\#mydestination = $myhostname, localhost.$mydomain, localhost
```

Be sure there are no dupes as the main.cf may have `**smtp_sasl_security_options = {}**` `, and` `**relayhost = {}**`.

Just delete or comment those lines.

Run `nano /etc/postfix/sasl_passwd` to create a password file:

```Plain
[smtp.gmail.com]:587 kjetil.furaas@gmail.com:PASSWD --> "See 1Password"
```

Run

```Bash
postmap hash:/etc/postfix/sasl_passwd
chmod 600 /etc/postfix/sasl_passwd
```

Restart service:

```Bash
systemctl restart postfix.service
```

Test:

```Bash
echo "Test mail from postfix" | mail -s "Test Postfix" kjetil.furaas@gmail.com
```

Logs:​

```Bash
/var/log/mail.warn
```

is helpful as well as

```Bash
/var/log/mail.info
```

## Check SMART status for Disks

Run `lsblk` to list disks

Run `smartctl -a /dev/DISK` to view information about  
disks  

## ZFS Alerts

Run `nano /etc/zfs/zed.d/zed.rc` and verify that this line  
is not commented out  
`ZED_EMAIL_ADDR="root"`

## If you are running a Proxmox host on a spare laptop

How to turn off laptop screen: Open “/etc/default/grub” and add `consoleblank=300` (time in seconds) to the `GRUB_CMDLINE_LINUX` property, e.g.:

```Plain
GRUB_CMDLINE_LINUX="consoleblank=300"
```

Then run `update-grub` to apply the new config for the next boot.

To turn off sleep mode when you close the laptop lid there’s an option in `/etc/systemd/logind.conf` that can help.

Uncomment the line `HandleLidSwitch=suspend` and change `suspend` to `ignore`.

Save and restart systemd-logind with `systemctl restart systemd-logind`

## Here is a solution to hibernate all VMs at reboot or shutdown

1. Go in proxmox shell, you need to be root.
2. vi /etc/init.d/proxmox
3. Add this code:

```Shell
#!/bin/shcase "$1" instart)   qm list | awk -F'[^0-9]*' '$0=$2' | while read -r vm_id; do qm unlock $vm_id; done;;;stop)   qm list | grep running | awk -F'[^0-9]*' '$0=$2' | while read -r vm_id; do qm suspend $vm_id --todisk 1; done;   sleep 10
;;esacexit 0
```

1. Run the following commands:

```Shell
chmod 755 /etc/init.d/proxmox
ln -s /etc/init.d/proxmox /etc/rc3.d/S99proxmox
ln -s /etc/init.d/proxmox /etc/rc0.d/K99proxmox
ln -s /etc/init.d/proxmox /etc/rc6.d/K99proxmox
systemctl daemon-reload
systemctl start proxmox
```

Don’t forget to add autostart option in proxmox to the VMs that have to boot on start.

You can reboot or shutown your server from: - Physical buttons -  
Proxmox Gui buttons - in shell : restart now / shutdown now  

## Disable ‘No valid subscription’ notice on Proxmox

To turn off the invalid subscription warning when opening Proxmox,  
use these steps:  

1. Open **Proxmox** server (web).
2. Select the server from the left navigation pane.
3. Click on **Shell**.
4. Type the following command to disable the subscription message.

```Shell
sed -Ezi.bak "s/(Ext.Msg.show\(\{\s+title: gettext\('No valid sub)/void\(\{ \/\/\1/g" /usr/share/javascript/proxmox-widget-toolkit/proxmoxlib.js && systemctl restart pveproxy.service
```

Once you complete the steps, the **You do not have a valid**  
**subscription for this server**  
message will no longer appear when  
logging in to the Proxmox server. However, if an update brings back the  
message, you will have to run the command again.  

When running the command from the web, the console will disconnect  
and reconnect after a few moments.