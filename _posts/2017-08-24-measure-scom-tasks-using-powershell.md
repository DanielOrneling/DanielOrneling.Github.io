---
title: "Measure SCOM Tasks using PowerShell"
date: "2017-08-24"
excerpt_separator: "<!--More-->"
categories: 
  - "operations-manager"
  - "orneling-se"
  - "powershell"
---

Sometimes when working with SCOM, one hears that “SCOM is slow” or “the console is taking forever to do this and that”. I won’t be speculating about the reason to why it might be slow with this post though, this could be to many reasons. But let´s say that you move your databases from one SQL Server to another for example, wouldn’t it be great to be able to measure the time it takes to execute several PowerShell commands both before and after the change to see the difference?

That´s exactly what I will provide in this post. In the beginning of the summer I came in a discussion about how to measure the performance of SCOM. Okay, this won´t give a complete picture of how the console works with but it will provide you with some valuable data.

It consists of a PowerShell script that you need to run from a management server or from a server that has the Operations Console installed.
<!--More-->
The commands that are measured are the following:

- Get-SCOMAgent
- Get-SCOMMonitoringObject
- Get-SCOMManagementPack
- Get-SCOMGroup
- Get-SCOMOverride
- Get-SCOMRule
- Get-SCOMMonitor
- Get-SCOMClass

As you can see, these are some powerful commands so it will take some time to complete depending on how big your environment is.

**Get started**

Start by downloading the script from TechNet Gallery [here](https://gallery.technet.microsoft.com/Measure-timing-of-SCOM-1a00439e?redir=0){:target="_blank"} and place it on a management server or a server that has the Operations Console installed.

The script looks like below:

<#
Author:  Daniel Örneling
Twitter: @DanielOrneling
Date:    30/6/2017
Script:  MeasureSCOMTasks.ps1
Version: 1.0
Description: Use this script to measure the time it takes to run some SCOM commands.
#>

# Connect to Operations Manager
Import-Module OperationsManager
New-SCOMManagementGroupConnection

# Time the collection of SCOM Agents information
Write-Host "Amount of seconds taken to go through the SCOM agents: " -NoNewline
$SCOMAgents = Measure-Command {Get-SCOMAgent}
Write-Host "$($SCOMAgents.TotalSeconds)" -ForegroundColor Green

# Time the collection of SCOM monitoring objects information
Write-Host "Amount of seconds taken to go through the SCOM monitoring objects: " -NoNewline
$SCOMObjects = Measure-Command {Get-SCOMMonitoringObject}
Write-Host "$($SCOMObjects.TotalSeconds)" -ForegroundColor Green

# Time the collection of management packs information
Write-Host "Amount of seconds taken to go through the SCOM management packs: " -NoNewline
$SCOMMPs = Measure-Command {Get-SCOMManagementPack}
Write-Host "$($SCOMMPs.TotalSeconds)" -ForegroundColor Green

# Time the collection of SCOM groups information
Write-Host "Amount of seconds taken to go through the SCOM groups: " -NoNewline
$SCOMGroups = Measure-Command {Get-SCOMGroup}
Write-Host "$($SCOMGroups.TotalSeconds)" -ForegroundColor Green

# Time the collection of overrides information
Write-Host "Amount of seconds taken to go through the SCOM overrides: " -NoNewline
$SCOMOverrides = Measure-Command {Get-SCOMOverride}
Write-Host "$($SCOMOverrides.TotalSeconds)" -ForegroundColor Green

# Time the collection of rules information
Write-Host "Amount of seconds taken to go through the SCOM rules: " -NoNewline
$SCOMRules = Measure-Command {Get-SCOMRule}
Write-Host "$($SCOMRules.TotalSeconds)" -ForegroundColor Green

# Time the collection of monitors information
Write-Host "Amount of seconds taken to go through the SCOM monitors: " -NoNewline
$SCOMMonitors = Measure-Command {Get-SCOMMonitor}
Write-Host "$($SCOMMonitors.TotalSeconds)" -ForegroundColor Green

# Time the collection of classes information
Write-Host "Amount of seconds taken to go through the SCOM classes: " -NoNewline
$SCOMClasses = Measure-Command {Get-SCOMClass}
Write-Host "$($SCOMClasses.TotalSeconds)" -ForegroundColor Green

**Run the script**

To run the script, launch a PowerShell session as an administrator and browse to the path where you´ve copied the script. 
![](https://blog.orneling.se/assets/images/2017/08/measure_scom_1.jpg)

Launch the script and you will see the result just like in the below picture:
![](https://blog.orneling.se/assets/images/2017/08/measure_scom_2.jpg)

**Summary**

There you go, you got the time it took to complete several commands through PowerShell. Now don´t let my numbers fool you, yes, my servers are running on SSD disks and have the performance they need. But I also have a very limited lab environment, so you will see something completely different when running this in your environment.

I have tried the script in both SCOM 2012 and SCOM 2016 so feel free to use it and modify it as you may like.

If you have any questions about the script, feel free to leave a comment and I´ll get back to you as soon as I can.
