## Setup NAT Switch in Hyper-V

```PowerShell
New-VMSwitch -SwitchName "SwitchName" -SwitchType External
Get-NetAdapter       // (note down ifIndex of the newly created switch as INDEX)
New-NetIPAddress -IPAddress 10.10.10.1 -PrefixLength 24 -InterfaceIndex <INDEX>
New-NetNat -Name "MyNATnetwork" -InternalIPInterfaceAddressPrefix 10.10.10.0/24
```

## Set up Static Address on Servers using Powershell

```PowerShell
# Define the parameters for IP configuration
$IPAddress = "10.10.10.10"
$PrefixLength = 24  # Corresponds to a subnet mask of 255.255.255.0
$DefaultGateway = "10.10.10.1"
$DnsServer = "8.8.8.8"  # Example: Google's public DNS

# Define the script block for setting network configurations
$ScriptBlock = {
    param(
        $IPAddress,
        $PrefixLength,
        $DefaultGateway,
        $DnsServer
    )
    # Fetch the active network adapter
    $Interface = Get-NetAdapter | Where-Object {$_.Status -eq "Up"}
    $InterfaceIndex = $Interface.ifIndex

    # Apply the new IP address configuration to the active network adapter
    New-NetIPAddress -InterfaceIndex $InterfaceIndex -IPAddress $IPAddress -PrefixLength $PrefixLength -DefaultGateway $DefaultGateway

    # Configure the DNS server address for the active network adapter
    Set-DnsClientServerAddress -InterfaceIndex $InterfaceIndex -ServerAddresses $DnsServer
}

# Execute the script block with the specified parameters
Invoke-Command -ScriptBlock $ScriptBlock -ArgumentList $IPAddress, $PrefixLength, $DefaultGateway, $DnsServer
```