Ctrl + Space = Bicep suggestions Bicep modules MS Learn: [Bicep modules - Azure Resource Manager | Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/modules)

```
–confirm-with-what-if -c
```

Instruct the command to run deployment What-If before executing the  
deployment. It then prompts you to acknowledge resource changes before  
it continues.  

–resource-group -g [Required]

The resource group to create deployment at.

–parameters -p

Supply deployment parameter values. Parameters may be supplied from a  
file using the  
`@{path}` syntax, a JSON string, or as  
<KEY=VALUE> pairs. Parameters are evaluated in order, so when a  
value is assigned twice, the latter value will be used. It is  
recommended that you supply your parameters file first, and then  
override selectively using KEY=VALUE syntax.  

–template-file -f

The path to the template file or Bicep file.

–mode

The deployment mode.

Allowed values: Complete, Incremental. Default: Incremental.

Generate ARM Template from Bicep

```Shell
bicep build -f "/older/storage.bicep"
```

Deploy Bicep file with Powershell

```PowerShell
New-AzResourceGroupDeployment -TemplateFile "older/storage.bicep" -ResourceGroupName RG-BicepDemo
```

Deploy Bicep file with “What If statement”

```PowerShell
New-AzResourceGroupDeployment -TemplateFile "older/storage.bicep" -ResourceGroupName RG-BicepDemo -Type 'Standard_GRS' -WhatIf
```

```Shell
az deployment group -f "older/storage.bicep" -g RG-BicepDemo -p type=Standard_GRS what-if
```

Deploy Bicep file with AZ CLI

```Shell
az deployment group create -g kf-rg -f "instrastructure/rsv.bicep" -p "instrastructure/rsv.parameters.json"
```

Deploy Bicep using Subscription deployment scope

```Shell
az deployment sub create --location norwayeast --template-file tmp/vault/main.bicep
```

Export Azure Resource Group to json file

```Shell
az group export --name "kf-rg" > main.json
```

Convert json to bicep

```Shell
az bicep decompile --file main.json
```

[[ALZ Bicep]]