---
title: "Let Powershell install the SCOM Prerequisites for you"
date: "2014-04-17"
excerpt_separator: "<!--More-->"
categories: 
  - "operations-manager"
---

Every time i get to install SCOM at a new customer, I get very excited because it´s a world of opportunities that opens up. One of the heaviest tasks before being able to install SCOM is to install all the Prerequisites on the management server.

Since this is a time consuming task i wanted to do this installation using Powershell instead. Since my colleague had aldready created a script for installing the DPM prerequisites, i borrowed his script and modified it to be able to install the SCOM prerequisites automatically.
<!--More-->
### What does the script do?

The script starts by creating a folder on the C drive where it will put the downloaded MSI files (System CLR Types for SQL Server 2012 and Report Viewer Controls). The features and roles that are installed covers the following SCOM roles:

- Management Server
- Operations Console
- Web Console

After all of the Windows features have been installed, the prerequisites for the Operations Console are next in line.

### What does the script look like?

Start-Transcript -Path c:transcript0.txt -noclobber

# This scripts needs unrestricted access
Write-Host "This scripts needs unrestricted access (Set-ExecutionPolicy Unrestricted.)" -ForegroundColor Green
Write-Host "The prereq setup for System Center 2012 R2 Operations Manager takes around 15 minutes depending on your internet speed" -ForegroundColor Green

# Setting the variables.
$folderpath0 = 'C:Source'
$ShareName = "Source$"

#Check if folder exists, if not, create it
if (Test-Path $folderpath0){
Write-Host "The folder $folderPath0 exists."
} else{
Write-Host "The folder $folderPath0 does not exist, creating..." -NoNewline
New-Item $folderpath0 -type directory | Out-Null
Write-Host "done!" -ForegroundColor Green
}

# Check if file exists, if not, download it
$file0 = $folderPath0+"SQLSysClrTypes.msi"
$file1 = $folderPath0+"Reportviewer.msi"

if (Test-Path $file0){
write-host "The file $file0 exists."
} else {

# Download System CLR Types for SQL Server 2012
Write-Host "System CLR Types for SQL Server 2012" -nonewline -ForegroundColor yellow
$clnt = New-Object System.Net.WebClient
$url = "http://download.microsoft.com/download/F/E/D/FEDB200F-DE2A-46D8-B661-D019DFE9D470/ENU/x64/SQLSysClrTypes.msi"
$clnt.DownloadFile($url,$file0)
Write-Host "done!" -ForegroundColor Green

}

if (Test-Path $file1){
write-host "The file $file1 exists."
} else {

# Download Microsoft Report Viewer 2012 Runtime
Write-Host "Microsoft Report Viewer 2012 Runtime" -nonewline -ForegroundColor yellow
$clnt = New-Object System.Net.WebClient
$url = "http://download.microsoft.com/download/F/B/7/FB728406-A1EE-4AB5-9C56-74EB8BDDF2FF/ENU/x86/ReportViewer.msi"
$clnt.DownloadFile($url,$file1)
Write-Host "done!" -ForegroundColor Green

}

# Install Windows Features.
Get-Module servermanager
Install-WindowsFeature -Name Web-Server
Install-WindowsFeature -Name Web-Default-Doc
Install-WindowsFeature -Name Web-Dir-Browsing
Install-WindowsFeature -Name Web-HTTP-Errors
Install-WindowsFeature -Name Web-Static-Content
Install-WindowsFeature -Name Web-Http-Logging
Install-WindowsFeature -Name Web-Request-Monitor
Install-WindowsFeature -Name Web-Stat-Compression
Install-WindowsFeature -Name Web-Filtering
Install-WindowsFeature -Name Web-Windows-Auth
Install-WindowsFeature -Name Web-Net-Ext
Install-WindowsFeature -Name Web-Net-Ext45
Install-WindowsFeature -Name Web-Asp-Net
Install-WindowsFeature -Name Web-ISAPI-Ext
Install-WindowsFeature -Name Web-ISAPI-Filter
Install-WindowsFeature -Name Web-Mgmt-Console
Install-WindowsFeature -Name Web-Metabase
Install-WindowsFeature -Name NET-Framework-Core
Install-WindowsFeature -Name NET-HTTP-Activation
Install-WindowsFeature -Name NET-WCF-HTTP-Activation45
Install-WindowsFeature -Name Windows-Identity-Foundation
Install-WindowsFeature -Name Telnet-Client

# Install System CLR Types for SQL Server 2012
Write-Host "Installing System CLR Types for SQL Server 2012.." -nonewline

$PSScriptRoot = Split-Path -Path $MyInvocation.MyCommand.Path

msiexec /qb /i "$folderPath0SQLSysClrTypes.msi" | Out-Null

Write-Host "done!" -ForegroundColor Green
Start-Sleep -s 10

# Install Microsoft Report Viewer 2012 Runtime
Write-Host "Microsoft Report Viewer 2012 Runtime.." -nonewline

$PSScriptRoot = Split-Path -Path $MyInvocation.MyCommand.Path

msiexec /qb /i "$folderPath0ReportViewer.msi" | Out-Null

Write-Host "done!" -ForegroundColor Green
Start-Sleep -s 10

Write-Host "The server needs to be restarted before you start the System Center 2012 R2 Operations Manager installation." -nonewline -BackgroundColor Black -ForegroundColor Red

Stop-Transcript

```

After the script has run and you´ve rebooted your server, you should be good to go with the SCOM installation. Don´t forget to check out the C:prereqslog.txt file where all of the progress has been logged during the execution of the script.

### Conclusion

Using this script can help you save a lot of time and the human factor is out of the picture. By automating the prereqs installation, the installation process goes a lot smoother and you can spend your time creating accounts or drinking coffee :)