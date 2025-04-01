**Terraform destroy is a command that allows you to destroy**  
**either a full stack (based on your TF files), or single resources, using**  
**the -target option.**  

```Plain
terraform state list
terraform destroy -target RESOURCE_TYPE.NAME
terraform destroy -target RESOURCE_TYPE.NAME -target RESOURCE_TYPE2.NAME
```

**Remove a Resource**

```Plain
terraform state rm module.foo.packet_device.worker[0]
```

**Remove a Module**

```Plain
terraform state rm module.foo
```

**List all resources**

```Plain
terraform state list
```

**Remove a singe resource from the state**

```Plain
terraform state rm <resource_to_be_deleted>
```

**Destroy the whole stack of resource(s)**

```Plain
terraform destroy
terraform apply -destroy

(Commented lines in the configuration file(s) will also destroy the resource(s) when you run terraform apply)
```

**azurerm_storage_account provider**

[terraform-provider-azurerm/storage_account.html.markdown  
at main · hashicorp/terraform-provider-azurerm · GitHub  
](https://github.com/hashicorp/terraform-provider-azurerm/blob/main/website/docs/r/storage_account.html.markdown)

Terraform Resource ID for NSG

```Plain
ID Example: "/subscriptions/b7f543e7-29f0-4e13-8b16-e8e94170be88/resourceGroups/cert-demo-rg/providers/Microsoft.Network/networkSecurityGroups/cert-demo-nsg"
```

Terraform Resource ID for Subnet

```Plain
ID Example: "/subscriptions/b7f543e7-29f0-4e13-8b16-e8e94170be88/resourceGroups/cert-demo-rg/providers/Microsoft.Network/virtualNetworks/cert-demo-vnet/subnets/cert-demo-snet"
```

Terraform Resource ID for NSG association

```Plain
ID Example: "/subscriptions/b7f543e7-29f0-4e13-8b16-e8e94170be88/resourceGroups/cert-demo-rg/providers/Microsoft.Network/virtualNetworks/cert-demo-vnet/subnets/cert-demo-snet"
```