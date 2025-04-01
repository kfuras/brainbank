## **Login to a spesified Azure tenant**

```Plain
Login-AzAccount -Tenant "TenantID"
```

## **Purge deleted secret from the key vault permanently**

```Plain
Remove-AzKeyVaultSecret -VaultName "VaultName" -Name ConnectionStrings--DefaultConnection -InRemovedState
```