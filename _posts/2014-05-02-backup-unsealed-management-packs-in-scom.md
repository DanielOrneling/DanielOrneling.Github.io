---
title: "Backup unsealed Management Packs in SCOM"
date: "2014-05-02"
excerpt_separator: "<!--More-->"
categories: 
  - "management-packs"
  - "operations-manager"
tags: 
  - "scom"
---

When Operations Manager has been up and running for a while, a couple of overrides MP’s are created that we don´t want to lose. A while back, I wrote a blog post about how to schedule a backup of the custom MP’s using Powershell and Task Scheduler. Since that script were a bit longer than necessary, I decided to erase some lines of code to make it an easier script. If you want to read the old blog post, you can find it [here](http://blog.orneling.se/2012/12/automatically-backup-unsealed-management-packs-in-scom-2012/){:target="_blank"}.
<!--More-->
### So what does the script do?

The script looks after all unsealed Management Packs and then exports them to a file-path that´s specified in the script. Then the script can schedule by using Task Scheduler. It needs a folder to run in, e.g. E:Backup.

### How to use the script

The script is below and the only thing that needs to be changed before executing the script is the file-path, which is bold in the text below.

```

param($ManagementServer)

Import-Module OperationsManager

New-SCOMManagementGroupConnection -ComputerName $ManagementServer

$Date = Get-Date -Format "yyyy-MM-dd"

$TodaysFolder = "E:Backup" + $Date

New-Item $TodaysFolder -ItemType directory -Force

$mp = Get-SCOMManagementPack | where {$_.Sealed -like "False"}

Export-SCOMManagementPack -ManagementPack $mp -Path $TodaysFolder

Set-Location -Path $TodaysFolder
```

Create a new task by using Windows Task Scheduler and follow these steps

- Right click “Task Scheduler Library” and choose “Create Task”
- In the General pane, Mark “Run whether user is loggen on or not” and “Run with highest privileges”
- You should also set the executing account to a service account, that way the script does not depend on a single persons account.
- In the Trigger pane, set the schedule. See below for an example.

![](https://blog.orneling.se/assets/images/2014/05/TaskSchedule.jpg)

- On the Actions pane, you need to tell the task what to do so click “New…” and then leave “Start a program” as it is.
- In Program/Script, paste C:WindowsSystem32WindowsPowerShellv1.0powershell.exe which is the default path to Powershell.exe
- In Arguments, paste the following line, edit the file-path to where you placed the script, and set your own Management Server name.

```

-Command "& E:BackupManagementPacksexport.ps1 -ServerName 'YourManagementServer' ; exit $LASTEXITCODE"
```

- Click OK two times and enter the password for the service account to create the task.

Now when the task is created, you can test run the task by right clicking it and choose “Run”. Now, check the folder you created earlier and your unsealed management packs should now be exported to a folder matching todays date.

### Wrap Up

This script is very easy to use and it makes the backup process completely automatic, something that at least makes me calm knowing that my changes in rules, monitors and overrides are safe. You can download the script from my OneDrive here. If there any questions about the script, don´t hesitate to leave a comment.
