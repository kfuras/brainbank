Get Bitlocker recovery password

```Plain
manage-bde -protectors -get c: -type RecoveryPassword
```

```PowerShell
(Get-BitLockerVolume -MountPoint C).KeyProtector
```

Change Bitlocker recovery password

```Plain
manage-bde -protectors -add c: -RecoveryPassword 000000-000000-000000-000000-000000-000000-000000-000000
```

```PowerShell
Add-BitLockerKeyProtector -MountPoint c: -RecoveryPasswordProtector 000000-000000-000000-000000-000000-000000-000000-000000
```

Delete a Bitlocker recovery password

```Plain
manage-bde -protectors -delete c: -id "{2456E68C-0A56-4D97-93BC-FCF40812B72C}"
```

```PowerShell
Remove-BitLockerKeyProtector -MountPoint c: -KeyProtectorId "{0B8A841E-D694-4D51-8C88-07819D9D7CC4}"
```