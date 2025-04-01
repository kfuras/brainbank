There’s a few pre-requisites for this:

- Wireless network using WPA2-Enterprise (or any flavour that uses  
    802.1x)  
    
- Active Directory domain already set up
- AD Certification Authority already set up (Enterprise CA)
- User accounts synced to Azure AD
- NPS installed and configured
- Devices Azure AD joined and enrolled in Intune

As part of this process we will be configuring a certificate  
template, installing the Intune Certificate Connector for Intune onto a  
server of your choosing and creating some configuration profiles.  

## Configuring the CA

First step is to configure a template on the CA server:

- Open the Certification Authority console, expand **Certificate**  
    **Templates**  
    , right click on the folder and  
    pick **Manage**. This will open the Certificate Templates  
    Console.  
    
- Find the **User** certificate template, right click on  
    it and select **Duplicate**.
- Name the template on the General tab, then on the Compatibility tab  
    set the Certification Authority to Windows Server 2008 R2, and the  
    Certificate Recipient to Windows 7/Server 2008 R2.  
    
- On the Request Handling tab, tick Allow private key to be exported.  
    This is required so that the the Intune connector can install the  
    private key onto the end user device.  
    
- On the Cryptography tab, make sure the minimum key size is  
    2048.  
    
- On the Subject Name tab, make sure you selected Supply in the  
    request.  
    
- On the Extensions tab, under Application Policies, make sure that  
    there are three entries - Client Authentication, Secure Email and  
    Encrypting File System.  
    
- On the Security tab, add the computer account of the server you will  
    be using for the Intune connector, with Read and Enroll permissions.  
    Click Apply to save the template, then close the console.  
    
- Back in the Certification Authority console, right click  
    on **Certificate Templates** and pick **New >**  
    **Certificate Template to issue**  
    . Select the template you just  
    created.  
    
- Finally we need to allow the server to manage certificates - open  
    the CA properties and add the computer account of the server that will  
    host the connector, with **Issue and Manage Certificates**  
    and **Request Certificates** permissions.
- If you don’t have your root CA certificate already exported, open  
    the CA properties, select the current certificate from the list and  
    click View Certificate. From there, you can go to the Details tab, click  
    Copy to File, and export it as Base64 encoded .cer file.  
    

## Installing the  
Certificate Connector for Intune  

We will need a service account to run the connector, assuming you  
don’t want it to run as SYSTEM. I’ve not tested it as SYSTEM, but  
unfortunately the documentation isn’t very clear on permissions - it  
basically states it needs to be an administrator account on the server,  
with Log on as a Service rights. If you’re trying to put this on a  
domain controller your only option would be to put the account in the  
Domain Admins group. Don’t forget to configure the Log on as a Service  
right within gpedit.msc.  

Open the Intune portal and go to [Tenant  
administration > Connectors and tokens > Certificate  
connectors  
](https://endpoint.microsoft.com/\#blade/Microsoft_Intune_DeviceSettings/TenantAdminConnectorsMenu/certConnectors). Click on Add, then follow the link and instructions to  
download the installer.  

Run the installer with administrative privileges on the server. Run  
through the steps and make sure you have selected at least PKCS on the  
list of features. As a minimum you should be picking PKCS and  
Certificate Revocation.  

Once you’ve completed the wizard and it has completed successfully,  
you should be able to refresh the Certificate connectors page and see  
your connector listed.  

## Deploying the AD CA Root  
Certificate  

You’ll need to install the CA root certificate into the Trusted Root  
store on your end user devices. We can do this using a configuration  
profile - in the Intune portal, go to   
[Devices  
> Configuration profiles  
](https://endpoint.microsoft.com/\#blade/Microsoft_Intune_DeviceSettings/DevicesMenu/configurationProfiles) and click on Create profile. Select the  
platform (Windows 10 and later), then Profile type: Templates >  
Trusted certificate. If you’re trying to deploy this to other devices,  
the profile type may be slightly different but it should be obvious  
which one is a trusted certificate.  

Run through the steps, uploading the CA root certificate’s .cer file  
you exported previously. Complete the assignments as required, and  
finish the wizard. In my case I’ve assigned this to a device group which  
contains my Surface devices.  

## NPS Network Policy

Assuming you already have a functional 802.1x Wi-Fi setup, you should  
have at least one Network Policy within NPS. Make sure that one of the  
authentication methods for this is “Microsoft: Smart Card or other  
certificate”. You don’t have to remove the other options - if you leave  
PEAP and Secured Password in then people will still be able to connect  
with their username/password as normal. We will be using a client side  
configuration profile to force the client to use a certificate.  

Double check which certificate NPS is using to identify itself -  
under Contraints > Authentication Methods, click on the various  
options and Edit. This should bring a window up which tells you the  
current certificate. If this is issued by your AD CA then you’ll have an  
easier time configuring the profiles, but it doesn’t have to be - mine  
is issued by DigiCert so I need to grab the root CA cert used (in this  
case, DigiCert Global Root CA) and repeat the previous steps to deploy  
this certificate to the devices.  

## Deploying the Certificate

We now need to create a PKCS Certificate configuration profile - in  
the Intune portal, go to   
[Devices  
> Configuration profiles  
](https://endpoint.microsoft.com/\#blade/Microsoft_Intune_DeviceSettings/DevicesMenu/configurationProfiles) and click on Create profile. Select the  
platform (Windows 10 and later), then Profile type: Templates > PKCS  
certificate.  

Fill out the fields as below - leave the defaults except for:

- Key Storage Provider: Enroll to Software KSP
- Certification authority: The FQDN of the CA server which will be  
    issuing the certificates. This can be the root or a subordinate server  
    (preferably subordinate as your root enterprise CA should be  
    offline)  
    
- Certification authority name: The name shown in the CA console,  
    usually DOMAIN-COMPUTERNAME-ca  
    
- Certificate template name: The name of the certificate template we  
    made earlier  
    
- Certificate type: User
- Subject alternative name: User principal name (UPN), Value:  
    {{UserPrincipalName}}  
    
- Extended key usage: Client Authentication, Secure Email (these two  
    can be added via the Predefined Value dropdown), and finally Encrypting  
    File System, 1.3.6.1.4.1.311.10.3.4. I’m not sure if you need the Secure  
    Email and EFS entries here but I had a lot of trouble getting the  
    Windows 10 device to auto select the certificate, and as they’re on the  
    cert - they can go in here too.  
    
    ![[attachments/CloudattachmentsPasted_image_20221116120736.png]]
    

If you want to assign a domain name as a SAN to the certificate  
enrollment:  

![[attachments/CloudattachmentsPasted_image_20221116121259.png]]

Assign the  
profile to the appropriate groups (you can target a device if you want  
to pick “all users on these devices”). Wait a while for your devices to  
update their configuration profiles (or click Sync in the portal) and  
you should start to see your CA issuing certificates. If you open mmc  
and add the Certificates (User) snap-in on a client device, you should  
see the certificate has appeared on the device.  

A quick note here, if your usernames and UPNs don’t match you may  
find that you can’t authenticate - i.e. your Pre-Win2000 username must  
be the same as the beginning of your UPN.  
  
`DOMAIN\myusername`,  
and   
`myusername@domain.tld`

## Creating the Wi-Fi Profile

Now in the Intune portal, go to [Devices  
> Configuration profiles  
](https://endpoint.microsoft.com/\#blade/Microsoft_Intune_DeviceSettings/DevicesMenu/configurationProfiles) and click on Create profile. Select the  
platform (Windows 10 and later), then Profile type: Templates >  
Wi-Fi. Follow through the steps and fill out the following settings:  

- Wi-Fi type: Enterprise
- Wi-Fi name (SSID): Your Wi-Fi SSID
- Connection name: The name you want to appear in Windows, usually the  
    same as the SSID  
    
- Connect automatically when in range: Yes
- Authentication mode: User
- EAP type: EAP-TLS (this is the “Microsoft: Smart Card or other  
    certificate” one you’ll have seen in NPS)  
    
- Server Trust: Certificate server names: The name of the certificate  
    the NPS server is using, e.g. radius.lab.katystech.blog  
    
- Root certificates for server validation: Find the root CA  
    certificate which issued the NPS server’s certificate (which you should  
    have uploaded earlier as a Trusted Certificate). If your server  
    certificate came from your AD CA, use your AD CA Root certificate.  
    
- Client Authentication: Authentication method: PKCS certificate
- Client certificate (Identity certificate): Select the PKCS  
    Certificate profile you created earlier  
    
- Root certificate for client authentication: Select the AD CA root  
    certificate you uploaded earlier  
    

Complete the steps and assign as required. In my case I assigned to  
the group containing the Surfaces. While you can assign this to devices  
(as I did), don’t expect this connection to work while nobody is logged  
on. It requires there to already be a suitable certificate on the user’s  
Personal store - when nobody is logged on, presumably it’s expecting  
SYSTEM to have a certificate.  

![[attachments/CloudattachmentsPasted_image_20221116120938.png]]

## Testing Your Device

You can have a look if your certificate has appeared either through  
the Certificates snap-in (within mmc.exe) or in  
PowerShell   
`Get-ChildItem Cert:\CurrentUser\My` which should  
show you a list of thumbprints and subjects.  

There should also be a wireless profile on the device - which you can  
view through Windows Settings > Wi-Fi > Known Networks, or by  
running   
`netsh wlan show profile` in a command prompt.

Clicking on the Wi-Fi connection menu in the action centre, you  
should be able to connect to the network without entering any  
credentials, and without confirming anything.  

## It’s not working, help!

I had a lot of issues getting this working which came down to  
certificates. Make sure you have got the correct certificate on the  
Wi-Fi profile. There are a few troubleshooting methods you can use  
here:  

- Export the profile from the device -  
    run   
    `netsh wlan export profile` to export the saved profiles  
    to XML, which you can then examine in a text editor.  
    
- If you’re constantly getting “Unable to connect because you need a  
    certificate to sign in” - and you definitely have the certificate on the  
    device - unassign the Wi-Fi profile from Intune, then once it has  
    disappeared from the device, manually create a Wi-Fi profile - go  
    through Control Panel (control.exe, not the new Settings), Network and  
    Sharing Centre, Set up a new connection or network, Manually configure  
    and edit the advanced settings. Play around with these until you get the  
    connection to either work, or give a different error.  
    
- If you’ve made a profile manually on the device, once you’ve got  
    that working, export it. Try and make the Intune profile have the same  
    settings, you can then double check this by exporting the profile again  
    once it’s applied to the device and comparing the two files. This helped  
    me determine whether I was using the correct CA certificate for server  
    validation.  
    
- Turn on auditing on the NPS server - in the command prompt,  
    run   
    `auditpol /set /subcategory:"Network Policy Server" /success:enable /failure:enable` and  
    check the Security log in Event Viewer. You’ll want to filter this to  
    just show the NPS related entries. Try connecting again and hopefully  
    you’ll see something useful in the log.  
    
- Finally, more of a niche case - if you’re getting NPS to forward  
    accounting packets to a filtering appliance as a means of identifying  
    who is who, you can manipulate the attributes that NPS passes. In my  
    case, we use Fortigate and it isn’t able to map a UPN to a user, it has  
    to be given a sAMAccountName/Pre-Win2000 logon. By using the attribute  
    manipulation we can replace the “@domain.tld” with a blank string. This  
    will only work if the first portion of the UPN is the same as the  
    sAMAccountName. This setting can be found within the Connection Request  
    Policy, under “Attributes”.