Get Resource ID from a Recovery Services Vault Policy

```PowerShell
$vault = Get-AzRecoveryServicesVault -ResourceGroupName ipunkt-setup-rg -Name ipunkt-application-vm-backup
Set-AzRecoveryServicesVaultContext -Vault $vaultGet-AzRecoveryServicesBackupProtectionPolicy -Name "ipunkt-application-vm" | Select-Object -ExpandProperty Id
```