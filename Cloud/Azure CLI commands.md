Want to get a random available IP address from a subnet in Azure? Use  
the command below!  

```Plain
(az network vnet subnet list-available-ips --name "subnet" --resource-group "resource_group" --vnet-name "virtual_network" | ConvertFrom-Json | Get-Random)
```