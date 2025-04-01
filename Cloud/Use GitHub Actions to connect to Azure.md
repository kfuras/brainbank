Create an Azure Active Directory application and service principal  
  

This command will output the AppId property which is your ClientId. The Id property is APPLICATION-OBJECT-ID, and it will be used for creating federated credentials with Graph API calls.  

```PowerShell
New-AzADApplication -DisplayName kf_sp_bicep_oidc
```

Create a service principal. Replace the $clientId with the AppId from your output.

This command generates output with a different Id and will be used in the next step.

The new Id is the ObjectId.

```PowerShell
$clientId = (Get-AzADApplication -DisplayName kf_sp_bicep_oidc).AppIdNew-AzADServicePrincipal -ApplicationId $clientId
```

Create a new role assignment. Beginning with Az PowerShell module version 7.x, New-AzADServicePrincipal no longer assigns the Contributor role to the service principal by default.

Replace $resourceGroupName with your resource group name, and $objectId with generated Id, or Scope to a subscription.

```PowerShell
$objectId = (Get-AzADServicePrincipal -DisplayName kf_sp_bicep_oidc).IdNew-AzRoleAssignment -ObjectId $objectId -RoleDefinitionName Contributor -Scope "/subscriptions/000-000-000-000-000"
```

Get the values for clientId, objectId, subscriptionId, and tenantId to use later in your GitHub Actions workflow.

```PowerShell
$clientId = (Get-AzADApplication -DisplayName kf_sp_bicep_oidc).AppId$subscriptionId = (Get-AzContext).Subscription.Id$tenantId = (Get-AzContext).Subscription.TenantId$objectId = (Get-AzADApplication -DisplayName kf_sp_bicep_oidc).Id
```

Add federated credentials - Replace APPLICATION-OBJECT-ID with the Id (generated while creating app) for your Azure Active Directory application. - Set a value for CREDENTIAL-NAME to reference later. - Set the subject. The value of this is defined by GitHub depending on your workflow: - Jobs in your GitHub Actions environment: repo:  
  
`< Organization/Repository >:environment:< Name >`  
- For Jobs not tied to an environment, include the ref path for  
branch/tag based on the ref path used for triggering the workflow: repo:  
  
`< Organization/Repository >:ref:< ref path>`.  
For example,  
  
`repo:n-username/ node_express:ref:refs/heads/my-branch or repo:n-username/ node_express:ref:refs/tags/my-tag`.  
- For workflows triggered by a pull request event: repo:  
  
`< Organization/Repository >:pull_request`.

```PowerShell
Invoke-AzRestMethod -Method POST -Uri 'https://graph.microsoft.com/beta/applications/000-000-000-000-000/federatedIdentityCredentials' -Payload  '{"name":"github_pipeline","issuer":"https://token.actions.githubusercontent.com","subject":"repo:kfuras/bicep:ref:refs/heads/main","description":"PipelineTesting","audiences":["api://AzureADTokenExchange"]}'
```