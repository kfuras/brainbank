### How to update HBA firmware

1. Boot into EFI shell
2. Execute the following command to list all devices `map`  
    The device in this case is **hd9b0b**
3. Execute the following command to switch into the USB device  
      
    `hd9b0b:`
4. Execute the following command to list all HBAs  
      
    `sas2flash.efi -listall`
5. Execute the following commands to flash firmware and bios as well as  
    target the correct HBA by ID  
      
    `sas2flash.efi -o -f 2118it.bin -b mtpsas2.rom -c 1``sas2flash.efi -o -f 2118it.bin -b mtpsas2.rom -c 2`

- **o** = Advanced command mode This switch enable  
    advanced command mode.  
    
- **f** = Firmware Update This switch flash firmware from  
    filename1  
    
- **b** = BIOS Update This switch flash a BIOS from  
    filename1  
    
- **c** = Controller Number Flag This switch select a  
    controller by num1  
    
- **listall** = List all This switch list information  
    about all adapters  
    

**Links:** [SAS2Flash Utility Quick  
Reference Guide  
](https://docs.broadcom.com/doc/12353205)

[How  
to Use UEFI Interactive Shell and Its Common Commands  
](https://linuxhint.com/use-uefi-interactive-shell-and-its-common-commands/)