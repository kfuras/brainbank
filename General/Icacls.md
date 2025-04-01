[icacls  
documentation  
](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/icacls)

```Plain
# Grants full control on disk/share ("Z:\") for group ("c2-demo-avd users") on all subdirectory and files
icacls z: /t /grant "c2-demo-avd users":(f)
```