---
title: "Set up and monitor Nano server"
date: "2016-05-17"
excerpt_separator: "<!--More-->"
categories: 
  - "operations-manager"
  - "orneling-se"
---

It´s been a while since I wrote anything now (5 weeks approximately, which is not okay) and it´s time to monitor Nano Server again. Due to some really annoying issues with my lab environment I have had major problems installing the latest technical preview of Windows Server and SCOM. But I decided to have the last laugh and now both Windows Server 2016 and SCOM 2016 are running on TP5 level.
<!--More-->
So what´s new in SCOM 2016 TP5?

- Monitor a broad range of network devices without requiring Operations Manager certification
- Monitor Nano Server deployments, including DNS and IIS roles
- Realize more than 2X scale improvement in monitoring UNIX/Linux servers
- Experience a more responsive application console, including the ability to navigate across different views and pivots without having to wait for the data to load
- Seamlessly discover, install and update required management packs right from the administration console
- Tune management packs, and alter the monitors and alerting rules – either at source level or group level – to reduce alert noise
- Plan and schedule maintenance windows for workloads without generating spurious alerts in Operations Manager console
- Utilize the Preferred Partner program to discover third-party management packs, authoring tools, dashboard utilities, etc., right from the Operations Manager console

The feature I´m going to dig into in this post is the “Monitor Nano Server deployments” part, which have been improved in TP5 and you´re now able to install the agent on to a Nano server through the discovery process in the SCOM console. If you have been reading my blog for a while you might know that I wrote a post some weeks ago about how to monitor Nano server using SCOM, but that was using SCOM 2016 TP4 so I will show the new and improved way here instead. Find that post [here](http://blog.orneling.se/2016/03/monitoring-nano-server-using-scom-2/){:target="_blank"}. To get going, I will use almost the same scripts as I did in the previous post, I have just made a few changes, like adding “-DeploymentType -Guest” (Guest or Host is available) and “-Edition -Standard” (Standard or Datacenter available as the server version). I have also gotten rid of the “Microsoft-OneCore-ReverseForwarders-Package” which isn´t a prerequsite anymore.

**Creating the Nano Image** Below is the script I used to create the Nano Image VHDX:

Set-Location -Path E:\\Media\\NanoIIS
Import-Module .\\NanoServerImageGenerator.psm1
 
$password = "Yourpassword"
$securepass = ConvertTo-SecureString -AsPlainText $password -Force
 
# Create the VHDX file with the below parameters - Change MediaPath to the path where you´ve extracted the Server 2016 TP5 media. - Also change the TargetPath and ComputerName to reflect the name of your new server.
 
New-NanoServerImage -MediaPath E:\\Media\\Server2016TP5 \`
-BasePath .\\Base \`
-TargetPath E:\\Media\\NanoIIS\\TBNANOIIS02.vhdx \`
-ComputerName TBNANOIIS02 \`
-DeploymentType Guest \`
-Edition Standard \`
-AdministratorPassword $securepass \`
-Packages 'Microsoft-NanoServer-IIS-Package' 

Now that you´ve fired off the script, you will see the below output and this may take some time. For me it took about 10 minutes to create the image. 
![](https://blog.orneling.se/assets/images/2016/05/1.jpg)

Now that the image has been created, we can look it up in the target folder which in this case is “E:\\Media\\NanoIIS”. 
![](https://blog.orneling.se/assets/images/2016/05/2.jpg)

**Creating and configuring the Nano Server.** After having moved the VHDX to the host and created a VM out of it, I launched the VM and logged on the recovery consoleof the Nano server and changed the IP address. The next step was to domain join the server and prepare it with firewall openings to be able to install the SCOM agent later on.

This is what the Nano server looked like just after I booted it up for the first time. Note the time stamp. 
!![](https://blog.orneling.se/assets/images/2016/05/3.jpg)

Below is the script I used to make the changes needed.

\# Connect to the remote server
$computer = "172.16.0.86"
$cred = Get-Credential (Credential "TBNANOIIS02\\Administrator") 
$session = New-PSSession -ComputerName $computer -Credential $cred 

Enter-PSSession -Session $session
 
# Open the firewall on the Nano server to be able to access it
netsh advfirewall firewall set rule group="File and Printer Sharing" new enable=yes

# Open the firewall on the Nano server to be able to remotely install the SCOM agent
netsh advfirewall firewall set rule group="Windows Remote Management" new enable=yes
netsh advfirewall firewall set rule group="Windows Remote Management (Compatibility)" new enable=yes
netsh advfirewall firewall set rule group="Remote Service Management" new enable=yes
netsh advfirewall firewall set rule group="Windows Management Instrumentation (WMI)" new enable=yes
netsh advfirewall firewall set rule group="Virtual Machine Monitoring" new enable=yes
netsh advfirewall firewall set rule group="Remote Event Log Management" new enable=yes

Exit-PSSession

# Provision the computer account in the domain
Set-Location C:\\Windows\\System32
djoin.exe /provision /domain "Orneling" /machine "TBNANOIIS02" /savefile .\\odjblob

Enter-PSSession -Session $session

# Copy the "odjblob" file from C:\\Windows\\System32 to the Nano server (C:\\Temp in this example) 
 
# Make sure the DNS address is correct, otherwise change it like below.
Set-DnsClientServerAddress -ServerAddresses "172.16.0.12" -InterfaceIndex 3 # Run Get-NetIPAddress to find the InterfaceIndex value
 
# Join the server to the domain
djoin /requestodj /loadfile C:\\Temp\\odjblob /windowspath c:\\windows /localos
 
Shutdown /r /t 10 # Set a time in seconds that suits you
Exit-PSSession

![](https://blog.orneling.se/assets/images/2016/05/4.jpg)

Okay, the server has booted again and let´s try to log in using domain credentials instead. 
![](https://blog.orneling.se/assets/images/2016/05/5.jpg)

And the server is domain joined. 
![](https://blog.orneling.se/assets/images/2016/05/6.jpg)

Now I´ll just verify that Domain Admins have been added to the local admin group on the server. 
![](https://blog.orneling.se/assets/images/2016/05/7.jpg)

Okay, just one more thing to change with the server. The time zone is completely wrong and should of course be changed. For this I used the same script as I did in the posts about Nano TP4.

The script to set the time zone:

\# Connect to the remote server
$computer = "TBNANOIIS02"
$cred = Get-Credential (Credential "ORNELING\\Administrator")
$session = New-PSSession -ComputerName $computer -Credential $cred
 
Enter-PSSession -Session $session
 
# Set the timezone to match your local time
function Get-TimeZone($Name)
{
 \[system.timezoneinfo\]::GetSystemTimeZones() | 
 Where-Object { $\_.ID -like "\*$Name\*" -or $\_.DisplayName -like "\*$Name\*" } | 
 Select-Object -ExpandProperty ID
} 
 
$timezone = Get-TimeZone Stockholm # Type in "your" capital and grab the time zone for that city.
 
tzutil.exe /s $timezone
 
# Reboot the server for the changes to take effect
Shutdown /r /t 5 # Set a time in seconds that suits you
Exit-PSSession

![](https://blog.orneling.se/assets/images/2016/05/8.jpg)

Log in again and you will now see the correct time setting. 
![](https://blog.orneling.se/assets/images/2016/05/9.jpg)

**Installing the SCOM agent on to the Nano Server** Now that the server has been configured and everything looks right, it´s time to try and install the SCOM agent onto it. Below is the steps I took to install it through the Discovery Wizard. 
![](https://blog.orneling.se/assets/images/2016/05/10.jpg)

Choose Servers Only and you will know right away if your Nano server can be discovered or not.
![](https://blog.orneling.se/assets/images/2016/05/11.jpg)

I created a simple query to scan my AD, I just used a \* as a wildcard. 
![](https://blog.orneling.se/assets/images/2016/05/12.jpg)

Domain admin credentials entered and will give me the access I need in the server. 
![](https://blog.orneling.se/assets/images/2016/05/13.jpg)

Okay, the server can be contacted. Let´s see if I can install the agent as well. 
![](https://blog.orneling.se/assets/images/2016/05/14.jpg)

Yup. A couple of seconds later the agent was installed on to the server without a single issue. 
![](https://blog.orneling.se/assets/images/2016/05/15.jpg)

And just to verify that the service is running, I picked up the status from the Nano server using PowerShell. 
![](https://blog.orneling.se/assets/images/2016/05/16.jpg)

**Summary** What you´ve seen in this post is how easy the SCOM team have made it to install the SCOM agent on to a Nano server in this technical preview release. Compared to the process you had to go through with TP4 to install the agent, this will not differ from the normal agent installation process other than the Nano server being installed in seconds instead of about a minute in many cases. I´m really looking forward to seeing the final release of SCOM 2016 which most likely isn´t far away now.

Have you started monitoring Nano server? If so, what do you think about it? If you have any questions, just leave a comment below.
