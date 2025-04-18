Alias cheat sheet

- “add” is an alias for “install”
- “view” is an alias for “show”
- “find” is an alias for “search”
- “ls” is an alias for “list”
- “update” is an alias for “upgrade”
- “remove” and “rm” are aliases for “uninstall
- “config” is an alias for “settings”

Bulk install applications via `winget import`

```PowerShell
winget import --import-application 'Path to JSON file' --ignore-versions
```

Upgrade all packages except excluded packages when running Powershell  
as Administrator  

```PowerShell
function Test-Administrator
{
    $user = [Security.Principal.WindowsIdentity]::GetCurrent();    (New-Object Security.Principal.WindowsPrincipal $user).IsInRole([Security.Principal.WindowsBuiltinRole]::Administrator)
}if (Test-Administrator) {class Software {    [string]$Name    [string]$Id    [string]$Version    [string]$AvailableVersion}$upgradeResult = winget upgrade | Out-String$lines = $upgradeResult.Split([Environment]::NewLine)# Find the line that starts with Name, it contains the header$fl = 0while (-not $lines[$fl].StartsWith("Name")){    $fl++}# Line $i has the header, we can find char where we find ID and Version$idStart = $lines[$fl].IndexOf("Id")$versionStart = $lines[$fl].IndexOf("Version")$availableStart = $lines[$fl].IndexOf("Available")$sourceStart = $lines[$fl].IndexOf("Source")# Now cycle in real package and split accordingly$upgradeList = @()For ($i = $fl + 1; $i -le $lines.Length; $i++){    $line = $lines[$i]    if ($line.Length -gt ($availableStart + 1) -and -not $line.StartsWith('-'))    {        $name = $line.Substring(0, $idStart).TrimEnd()        $id = $line.Substring($idStart, $versionStart - $idStart).TrimEnd()        $version = $line.Substring($versionStart, $availableStart - $versionStart).TrimEnd()        $available = $line.Substring($availableStart, $sourceStart - $availableStart).TrimEnd()        $software = [Software]::new()        $software.Name = $name;        $software.Id = $id;        $software.Version = $version        $software.AvailableVersion = $available;        $upgradeList += $software    }}$upgradeList | Format-Table$toSkip = @('Microsoft.Office','Microsoft.Teams','Discord.Discord','VMware.WorkstationPro''TeamViewer.TeamViewer.Host')foreach ($package in $upgradeList){    if (-not ($toSkip -contains $package.Id))    {        Write-Host "Going to upgrade package $($package.id)"        & winget upgrade $package.id    }    else    {        Write-Host "Skipped upgrade to package $($package.id)"    }}}
```