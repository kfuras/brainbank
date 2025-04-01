# Ubuntu: How To Free Up Port 53, Used By systemd-resolved

[Logix](https://draft.blogger.com/profile/03026963810377267607)  Updated on [July 6, 2020](https://www.linuxuprising.com/2020/07/ubuntu-how-to-free-up-port-53-used-by.html) [dns](https://www.linuxuprising.com/search/label/dns?max-results=14), [how-to](https://www.linuxuprising.com/search/label/how-to?max-results=14), [network](https://www.linuxuprising.com/search/label/network?max-results=14), [systemd](https://www.linuxuprising.com/search/label/systemd?max-results=14), [ubuntu](https://www.linuxuprising.com/search/label/ubuntu?max-results=14)

[![](https://www.linuxuprising.com/ezoimgfmt/1.bp.blogspot.com/-WTci5YOGahk/XwNFanRo65I/AAAAAAAAEoo/nK88yA8-9KkkreY7b4TlOHfvJUfZI2SGACLcBGAsYHQ/s640/systemd-resolved-port-53.png?ezimgfmt=rs%3Adevice%2Frscb273-1)](https://www.linuxuprising.com/ezoimgfmt/1.bp.blogspot.com/-WTci5YOGahk/XwNFanRo65I/AAAAAAAAEoo/nK88yA8-9KkkreY7b4TlOHfvJUfZI2SGACLcBGAsYHQ/s640/systemd-resolved-port-53.png?ezimgfmt=rs%3Adevice%2Frscb273-1)

Ubuntu has systemd-resolved listening on port 53 by default. In case you want to run your own DNS server, you can’t because port 53 is already in use, so you’ll get an error similar to this: “listen tcp 0.0.0.0:53: bind: address already in use”.  

- *This article explains how to stop systemd-resolved from using port 53 on Ubuntu. The instructions were tested on Ubuntu 20.04, but they should also work on other Ubuntu versions, e.g. Ubuntu 18.04, the upcoming Ubuntu 20.10, as well as Ubuntu-based Linux distributions like Pop!_OS, Zorin OS, Elementary OS, Linux Mint, and so on.** Basically, this works on any system having systemd version 232 or newer. 

To see if port 53 is in use on your system, use:

```Plain
sudo lsof -i :53
```

Example with output, showing that systemd-resolved is using port 53  
on a default Ubuntu 20.04 system:  

```Plain
$ sudo lsof -i :53

COMMAND   PID            USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
systemd-r 610 systemd-resolve   12u  IPv4  19377      0t0  UDP localhost:domain
systemd-r 610 systemd-resolve   13u  IPv4  19378      0t0  TCP localhost:domain (LISTEN)
```

In case you don’t get any output, it means that port 53 is not in use.  

## How to stop systemd-resolved from using port 53 on Ubuntu

It’s worth noting that you can free up port 53 by simply uncommenting `DNSStubListener` and setting it to `no` in `/etc/systemd/resolved.conf`. 
The other steps are for enabling a DNS server - without it, your system will not  
be able to resolve any domain names, so you won’t be able to visit websites in web browser, etc.  

**1.** Edit `/etc/systemd/resolved.conf` with a text editor (as root), e.g. open it with Nano console text editor:  

```Plain
sudo nano /etc/systemd/resolved.conf
```

And uncomment (remove `#` from the front of the line) the `DNS=` line and the `DNSStubListener=` line. Next, change the `DNS=` value in this file to the DNS server you want to use (e.g. 127.0.0.1 to use a local proxy, 1.1.1.1 to use the  
Cloudflare DNS, etc.), and also change the `DNSStubListener=` value from `yes` to `no`.

This is how the file should look after you’ve made these changes (I’m using 1.1.1.1 as the DNS server here, which is the Cloudflare DNS):  

```Plain
[Resolve]
DNS=1.1.1.1
\#FallbackDNS=
\#Domains=
\#LLMNR=no
\#MulticastDNS=no
\#DNSSEC=no
\#DNSOverTLS=no
\#Cache=no
DNSStubListener=no
\#ReadEtcHosts=yes
```

To save the file using Nano text editor, press `Ctrl + x`,  
then type   
`y` and press `Enter`.

**2.** Create a symbolic link  
for   
`/run/systemd/resolve/resolv.conf` with `/etc/resolv.conf` as  
the destination:  

```Plain
sudo ln -sf /run/systemd/resolve/resolv.conf /etc/resolv.conf
```

Here, `-s` is for creating a symbolic and not hard link,  
and   
`-f` is for removing any existing destination files (so  
it removes   
`/etc/resolv.conf` if it exists).

**3.** Reboot your system.

Port 53 should now be free on your Ubuntu system, and you shouldn’t  
be getting errors like “listen tcp 127.0.0.1:53: bind: address already  
in use” anymore.  

You can check to see if port 53 is in use or not by  
running   
`sudo lsof -i :53` - if port 53 is not in use, this  
command shouldn’t show any output.  

## How to undo the changes

Do you want to undo the changes made by following the instructions in  
this article? This is what you must do.  

**1.** Start by  
editing   
`/etc/systemd/resolved.conf` with a text editor (as  
root), e.g. open it with Nano console text editor:  

```Plain
sudo nano /etc/systemd/resolved.conf
```

And comment out (add `#` in front of the  
line)   
`DNS=` and `DNSStubListener=no`, then save  
the file. To save the file using Nano text editor,  
press   
`Ctrl + x`, then type `y` and  
press   
`Enter`.

**2**. Remove the `/etc/resolv.conf` symbolic  
link:  

```Plain
sudo rm /etc/resolv.conf
```

**3**. Reboot your system.