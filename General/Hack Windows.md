## Forgot Windows Admin Password? Unlock Your PC with These Commands

- Get the Bitlocker recovery key from Azure or Microsoft account,  
    URL:  
    [Device  
    List  
    ](https://myaccount.microsoft.com/device-list)
- Boot into recovery mode - Press and hold shift then click restart  
    from start menu. From the blue **Choose an option** screen  
    press **Troubleshoot** - **Advanced Options**  
    - **Command Prompt**
- When you see the **Bitlocker** screen type in the  
    **Bitlocker recovery key** from earlier, the command prompt  
    will open, run the following commands to swap sticky keys with  
    cmd  
    

```Plain
c:
cd windows\system32
copy sethc.exe ..
copy cmd.exe sethc.exe
```

- Type **Exit** to close command prompt, this will  
    return you to the blue **Choose an option** screen, press  
    **Continue** to boot into Windows
- When at the windows login screen, reboot into safe mode - Press  
    and hold shift then click restart from start menu. From the blue  
    **Choose an option** screen press  
    **Troubleshoot** - **Advanced Options** -  
    **Startup Settings** and **Restart**, wait for  
    the blue **Startup Settings** screen to show, select  
    **Safe Mode**
- Press the **shift key 5 times** to open up command  
    prompt as administrator, then run the following:  
    

```Plain
net user 'username' 'password' /add
net localgroup administrators 'username' /add
```

- Close command prompt and boot back into Windows again
- To unhack windows (restore sethc.exe to the original place) run the following  
    command:  
    

```Plain
robocopy c:\windows c:\windows\system32 sethc.exe /B
```