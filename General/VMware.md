The default behavior of the ESXi 8.0 installer is to prevent users  
from installing ESXi on a system that has a CPU that is not officially  
supported.  

**ProTip:** With that said, there is a workaround for  
those that wish to forgo official support from VMware or for homelab and  
testing purposes, you can add the following ESXi kernel option  
(SHIFT+O):  

`allowLegacyCPU=true`

which will turn the error message into a warning message and enable  
the option to install ESXi, knowing that the CPU is not officially  
supported and accept any risks in doing so.  

### With ESXi 7.0 Update 1c System storage consumes a default of 138GB if  
systemMediaSize is not provided. It is the recommended size for most  
servers. Fore more information refer to   
[ESXi  
7.0 Update1c release notes  
](https://docs.vmware.com/en/VMware-vSphere/7.0/rn/vsphere-esxi-70u1c.html\#whatsnew)

The systemMediaSize boot option accepts the following parameters with  
the corresponding size used for ESXi system partitions:  

- min 33GB, for single disk or embedded servers
- small 69GB, for servers with at least 512GB RAM
- max all available space, for multi-terabyte servers

**Note**: GB units specified are in storage device  
sizes, i.e. 1,000,000,000 byte multiples  

Boot options can be provided to the installer in various ways  
depending on what install method is used (refer to the links in the  
Related Information section for more detail). There are two methods  
below for providing the boot option at startup and apply to any chosen  
installer media.  

## **Entering**  
**the boot option at boot media startup**  
:

- Start the host with the install image and when the ESXi installer  
    window appears, press **Shift+O** within 5 seconds to edit  
    the boot options.  
    

For example, add the following prompt:

`systemMediaSize=small`

## **Modifying**  
**boot.cfg to have the boot option:**  

Edit the boot.cfg file in the install image and add the boot options  
to the kernelopt line.  

For  
example,   
`kernelopt=runweasel systemMediaSize=small`