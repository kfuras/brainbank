Get Log Analytics setting categories

```PowerShell
$ResourceId = "/subscriptions/0-0-0-0-0/resourceGroups/hub-prod-network-resources/providers/Microsoft.Network/azureFirewalls/hub-westeurope-network-fw"$DiagnosticSettingCategories = Get-AzDiagnosticSettingCategory -ResourceId $ResourceId$DiagnosticSettingCategories
```