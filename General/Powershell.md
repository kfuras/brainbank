Add a user to a local group using powershell

```PowerShell
Add-LocalGroupMember -Group GroupName -Member Domain\UserName
```

Add multiple users to a local group separated by comma using  
powershell  

```PowerShell
Add-LocalGroupMember -Group GroupName -Member Domain\UserName, Domain\UserName2
```

Add a local user or a AD user to the remote computer,  
use **Invoke-Command**

```PowerShell
Invoke-Command -ComputerName Computer1, Computer2 -ScriptBlock {Add-LocalGroupMember -Group GroupName -Member Domain\UserName, Domain\UserName2
}
```

Get the PowerShell PSReadlineOption command history file  
location:  

```PowerShell
(Get-PSReadlineOption).HistorySavePath
```

Show the contents of the PowerShell PSReadlineOption command history  
file:  

```PowerShell
cat (Get-PSReadlineOption).HistorySavePath
```

Clear the command history in PowerShell PSReadlineOption by deleting  
the history file:  

```PowerShell
Remove-Item (Get-PSReadlineOption).HistorySavePath
```

Change how PowerShell PSReadlineOption command history is saved:

```PowerShell
Set-PSReadlineOption -HistorySaveStyle SaveIncrementally # defaultSet-PSReadlineOption -HistorySaveStyle SaveAtExit
Set-PSReadlineOption -HistorySaveStyle SaveNothing
```

Filter on a regular expression pattern and output the filtered data,  
using PowerShell.  

We Invoke a PowerShell command that stores it’s data in a variable  
called  
`$KOSMOSLOG`.

```PowerShell
$KOSMOSLOG = Invoke-AzVMRunCommand -ResourceGroupName "ipunkt-setup-rg" -VMName "ipunkt-application-vm" -CommandId 'RunPowerShellScript' -ScriptString "Get-Content -Tail 145 'C:\integrasjonspunkt\kosmos-logs\kosmos-service.out.log'"
```

The variable contains the following data:

```PowerShell
"Value[0]        :  Code          : ComponentStatus/StdOut/succeeded  Level         : Info  DisplayStatus : Provisioning succeeded  Message       : -14 17:26:26.639  INFO 4380 --- [           main] n.d.m.k.s.launcher.LauncherServiceImpl   : Waitingfor health check to pass2023-06-14 17:26:27.686  INFO 4380 --- [           main] n.d.m.k.s.launcher.LauncherServiceImpl   : Waiting for healthcheck to pass2023-06-14 17:26:28.826  INFO 4380 --- [           main] n.d.m.k.s.launcher.LauncherServiceImpl   : Waiting for healthcheck to pass2023-06-14 17:26:29.889  INFO 4380 --- [           main] n.d.m.k.s.launcher.LauncherServiceImpl   : Waiting for healthcheck to pass2023-06-14 17:26:31.170  INFO 4380 --- [           main] n.d.m.k.s.launcher.LauncherServiceImpl   : Waiting for healthcheck to pass2023-06-14 17:26:32.342  INFO 4380 --- [           main] n.d.m.k.s.launcher.LauncherServiceImpl   : Waiting for healthcheck to pass2023-06-14 17:26:33.764  INFO 4380 --- [           main] n.d.m.k.s.launcher.LauncherServiceImpl   : Waiting for healthcheck to pass2023-06-14 17:26:34.983  INFO 4380 --- [           main] n.d.m.k.s.launcher.LauncherServiceImpl   : Waiting for healthcheck to pass2023-06-14 17:26:36.108  INFO 4380 --- [           main] n.d.m.k.s.launcher.LauncherServiceImpl   : Waiting for healthcheck to pass2023-06-14 17:26:37.342  INFO 4380 --- [           main] n.d.m.k.s.launcher.LauncherServiceImpl   : Waiting for healthcheck to pass2023-06-14 17:26:38.686  INFO 4380 --- [           main] n.d.m.k.s.launcher.LauncherServiceImpl   : Waiting for healthcheck to pass2023-06-14 17:26:39.905  INFO 4380 --- [           main] n.d.m.k.s.launcher.LauncherServiceImpl   : Waiting for healthcheck to pass2023-06-14 17:26:46.077  WARN 4380 --- [ctor-http-nio-2] r.netty.http.client.HttpClientConnect    : [id: 0xf1e33efb, L:/127.0.0.1:49937 - R:localhost/127.0.0.1:9093] The connection observed an error io.netty.handler.timeout.ReadTimeoutException: null2023-06-14 17:26:46.093  INFO 4380 --- [           main] n.d.m.k.s.launcher.LauncherServiceImpl   : Waiting for healthcheck to pass2023-06-14 17:26:50.890  INFO 4380 --- [           main] n.d.m.k.s.launcher.LauncherServiceImpl   : Waiting for healthcheck to pass2023-06-14 17:26:52.219  INFO 4380 --- [           main] n.d.m.k.s.launcher.LauncherServiceImpl   : Application started successfully!2023-06-14 17:26:52.219  INFO 4380 --- [           main] n.d.m.k.action.application.StartAction   : Blocklist mechanism is disabled2023-06-14 17:26:52.219  INFO 4380 --- [           main] n.d.m.k.action.application.StartAction   : Launch success, the version 2.19.0 will be Allowlisted2023-06-14 17:26:52.265  INFO 4380 --- [           main] n.d.m.k.action.application.StartAction   : Upgrade SUCCESS integrasjonspunkt-2.19.0.jar2023-06-14 17:26:52.609  INFO 4380 --- [           main] n.d.m.k.handler.SynchronizationHandler   : Finished synchronization2023-06-14 17:26:52.640  WARN 4380 --- [           main] c.n.c.sources.URLConfigurationSource     : No URLs will be polled as dynamic configuration sources.2023-06-14 17:26:55.125  WARN 4380 --- [           main] ockingLoadBalancerClientRibbonWarnLogger : You already have RibbonLoadBalancerClient on your classpath. It will be used by default. As Spring Cloud Ribbon is in maintenance mode. We recommend switching to BlockingLoadBalancerClient instead. In order to use it, set the value of `spring.cloud.loadbalancer.ribbon.enabled` to `false` or remove spring-cloud-starter-netflix-ribbon from your project.2023-06-14 17:26:55.172  WARN 4380 --- [           main] eactorLoadBalancerClientRibbonWarnLogger : You have RibbonLoadBalancerClient on your classpath. LoadBalancerExchangeFilterFunction that uses it under the hood will be used by default. Spring Cloud Ribbon is now in maintenance mode, so we suggest switching to ReactorLoadBalancerExchangeFilterFunction instead. In order to use it, set the value of `spring.cloud.loadbalancer.ribbon.enabled` to `false` or remove spring-cloud-starter-netflix-ribbon from your project.2023-06-14 17:26:55.266  INFO 4380 --- [           main] no.difi.move.kosmos.KosmosMain           : Started KosmosMainin 151.696 seconds (JVM running for 155.881)Value[1]        :  Code          : ComponentStatus/StdErr/succeeded  Level         : Info  DisplayStatus : Provisioning succeeded  Message       :Status          : SucceededCapacity        : 0Count           : 0"
```

To filter and display only the lines that contains the strings you  
want in the  
`$KOSMOSLOG` variable, you can use the following  
code:  

```PowerShell
$KOSMOSLOG = Invoke-AzVMRunCommand -ResourceGroupName "ipunkt-setup-rg" -VMName "ipunkt-application-vm" -CommandId 'RunPowerShellScript' -ScriptString "Get-Content -Tail 145 'C:\integrasjonspunkt\kosmos-logs\kosmos-service.out.log'"$KOSMOSLOG.Value[0].Message -split '\r?\n' | Where-Object { $_ -match 'n\.d\.m\.k\.action\.application\.StartAction|n\.d\.m\.k\.s\.launcher\.LauncherServiceImpl|c\.n\.c\.sources\.URLConfigurationSource' }
```

The `-split` operator is used to split a string into an  
array of substrings based on a specified delimiter. In this case, the  
delimiter is  
`\r?\n`, which represents a newline  
character.  

Let’s break down the meaning of `\r?\n`:

- `\r` represents the carriage return character, which is  
    commonly used in old-style Windows line breaks.  
    
- `?` is a quantifier that makes the preceding  
      
    `\r` optional. It allows for flexibility in handling  
    different line break formats.  
    
- `\n` represents the newline character, which is commonly  
    used for line breaks in Unix-like systems.  
    

By using `\r?\n` as the delimiter, the `-split`  
operator will split the input string into separate lines, regardless of  
the specific line break format used in the input.  

This code uses the `Where-Object` cmdlet to filter the  
lines from  
`$KOSMOSLOG` based on a regular expression  
pattern. The  
`-match` operator is then used to match lines  
that contains the following. -  
  
`n.d.m.k.action.application.StartAction` -  
  
`n.d.m.k.s.launcher.LauncherServiceImpl` -  
  
`n.d.m.k.handler.SynchronizationHandler`

The patterns are provided as regular expressions, where the dots  
(  
`.`) are escaped with backslashes (`\`) to match  
them literally. The pipe (  
`|`) character is used as an OR  
operator to search for either pattern.