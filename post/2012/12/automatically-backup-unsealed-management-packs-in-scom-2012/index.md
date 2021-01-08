---
title: "Automatically backup unsealed Management Packs in SCOM 2012"
date: "2012-12-20"
categories: 
  - "operations-manager"
tags: 
  - "microsoft"
  - "operations-manager"
  - "system-center"
---

After creating several overrides that is stored in unsealed Management Packs, they get more important to you in case of a failure.The script that you can find below takes a copy of all unsealed Management Packs and stores them in a folder that is set in the script, in this case “D:Backup”.

I have borrowed the script from [http://systemcenter.no/?p=195](http://systemcenter.no/?p=195 "Systemcenter.no") and then made some modifications to the script that you can find below. **Before executing the script**

In order for this to work, cange the $TodaysFolder in the script to your own folder and save it to_export.ps1_ for example.

### Executing the script

To execute the script, open Powershell and browse to the directory where the script is stored and run the following command:

```

export.ps1 ServerName:Management Server

param ($ServerName)

add-pssnapin “Microsoft.EnterpriseManagement.OperationsManager.Client”;

set-location “OperationsManagerMonitoring::”;

new-managementGroupConnection -ConnectionString:$ServerName;

set-location $ServerName;

$Date = Get-Date -Format “yyyy-MM-dd”
$TodaysFolder = “D:BACKUP” + $Date
New-Item $TodaysFolder -type directory -force
$mps = get-managementpack | where-object {$_.Sealed -eq $false}

foreach ($mp in $mps)

{

export-managementpack -managementpack $mp -path $TodaysFolder

}
Set-location -path $TodaysFolder

remove-pssnapin “Microsoft.EnterpriseManagement.OperationsManager.Client”;
```

### Running the script via Windows Task Scheduler

Open Task scheduler Right click Task Scheduler Library and choose “Create Task…” Name the Task Mark “Run wether user is logged on or not” Go to the Triggers tab and choose “New…” Set the schedule for your task to once per day or less often Click on the Actions Tab and click “New…” In Action, choose Start a program and then go to “Program/Script” C:WindowsSystem32WindowsPowerShellv1.0powershell.exe is the default path for Powershell.exe Go on to Add arguments (optional) and paste the following after editing the path to the script and your Managenent Server name -Command “& Pathexport.ps1 -ServerName ‘ManagementServerName‘ ; exit $LASTEXITCODE” If the above does´nt work, make sure the task is run by a user with administrativ privileges on the server where the task is run. This can be done under the General tab in Task properties and then choosing “Change User or Group…”.
