[Verify encryption status for Linux - Azure Disk Encryption - Azure Virtual Machines | Microsoft Learn](https://learn.microsoft.com/en-us/azure/virtual-machines/linux/how-to-verify-encryption-status\#powershell)

OSDisk

```PowerShell
$RGName = "RGName"$VMName = "VMName"$VM = Get-AzVM -Name ${VMName} -ResourceGroupName ${RGName}$Sourcedisk = Get-AzDisk -ResourceGroupName ${RGName} -DiskName $VM.StorageProfile.OsDisk.NameWrite-Host "============================================================================================================="Write-Host "Encryption Settings:"Write-Host "============================================================================================================="Write-Host "Enabled:" $Sourcedisk.EncryptionSettingsCollection.EnabledWrite-Host "Version:" $Sourcedisk.EncryptionSettingsCollection.EncryptionSettingsVersionWrite-Host "Source Vault:" $Sourcedisk.EncryptionSettingsCollection.EncryptionSettings.DiskEncryptionKey.SourceVault.IdWrite-Host "Secret URL:" $Sourcedisk.EncryptionSettingsCollection.EncryptionSettings.DiskEncryptionKey.SecretUrlWrite-Host "Key URL:" $Sourcedisk.EncryptionSettingsCollection.EncryptionSettings.KeyEncryptionKey.KeyUrlWrite-Host "============================================================================================================="
```

DataDisks

```PowerShell
$RGName = "RGName"$VMNAME = "VMName"
$VM = Get-AzVM -Name ${VMName} -ResourceGroupName ${RGName}Clear-Host
foreach ($i in $VM.StorageProfile.DataDisks|ForEach-Object{$_.Name})
{ Write-Host "==========================================================================================================="Write-Host "Encryption Settings:"
Write-Host "============================================================================================================="
Write-Host "Checking Disk:" $i $Disk=(Get-AzDisk -ResourceGroupName ${RGName} -DiskName $i)Write-Host "Encryption Enable: " $Sourcedisk.EncryptionSettingsCollection.Enabled
Write-Host "Encryption KeyEncryptionKey: " $Sourcedisk.EncryptionSettingsCollection.EncryptionSettings.KeyEncryptionKey.KeyUrl;Write-Host "Encryption DiskEncryptionKey: " $Sourcedisk.EncryptionSettingsCollection.EncryptionSettings.DiskEncryptionKey.SecretUrl;Write-Host "============================================================================================================="}
```