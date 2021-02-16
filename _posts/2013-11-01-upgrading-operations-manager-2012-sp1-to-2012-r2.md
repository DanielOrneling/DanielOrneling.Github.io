---
title: "Upgrading Operations Manager 2012 SP1 to 2012 R2"
date: "2013-11-01"
excerpt_separator: "<!--More-->"
categories: 
  - "operations-manager"
---

As most people (at least IT people) knows, Microsoft made System Center 2012 R2 generally available about two weeks ago and now the time has finally come for me to upgrade from SCOM 2012 SP1 to R2 instead.

The environment I´m upgrading today consists of two servers, one DB server and one Management Server. The first thing i did was to apply all Windows Updates (including CU4 for Operations Manager) to make sure their running at the latest patch level. Before we can fire off the upgrade, there are a few steps to walk through.
<!--More-->
### Pre-Upgrade Tasks

The first step is to cleanup the database and to manually run the grooming process. The setup does this automatically with a script but to make the installation smoother, It can be run manually by using the script below. The script is most important if there are over 100.000 rows, I had 3472 rows but i used the script anywayto cleanup the tables.

Determine the amount of rows

```
DECLARE @SubscriptionWatermark bigint = 0;     SELECT @SubscriptionWatermark = dbo.fn_GetEntityChangeLogGroomingWatermark(); Select COUNT (*) FROM EntityTransactionLog ETL with(nolock) WHERE NOT EXISTS (SELECT 1 FROM EntityChangeLog ECL with(nolock) WHERE ECL.EntityTransactionLogId = ETL.EntityTransactionLogId) AND NOT EXISTS (SELECT 1 FROM RelatedEntityChangeLog RECL with(nolock) WHERE RECL.EntityTransactionLogId = ETL.EntityTransactionLogId) AND EntityTransactionLogId < @SubscriptionWatermark;
```

Cleanup the tables

```
DECLARE @RowCount int = 1; DECLARE @BatchSize int = 100000; DECLARE @SubscriptionWatermark bigint = 0; DECLARE @LastErr int; SELECT @SubscriptionWatermark = dbo.fn_GetEntityChangeLogGroomingWatermark(); WHILE(@RowCount > 0) BEGIN DELETE TOP (@BatchSize) ETL FROM EntityTransactionLog ETL WHERE NOT EXISTS (SELECT 1 FROM EntityChangeLog ECL WHERE ECL.EntityTransactionLogId = ETL.EntityTransactionLogId) AND NOT EXISTS (SELECT 1 FROM RelatedEntityChangeLog RECL WHERE RECL.EntityTransactionLogId = ETL.EntityTransactionLogId) AND ETL.EntityTransactionLogId < @SubscriptionWatermark; SELECT @LastErr = @@ERROR, @RowCount = @@ROWCOUNT; END
```

Remove agents from pending state

In my case, i applied CU4 prior to the R2 upgrade which resulted in my agents needing an update. Make sure that the agent pending tab in SCOM is empty by approving all of the pending agents.

Disable connectors

If there are any connectors made to Service Manager for example, disable them to avoid issues with the connectors during the upgrade. Another important thing, if there are connectors made between the different System Center products you might want to check [this link](http://technet.microsoft.com/en-us/library/dn521010.aspx){:target="_blank"} out. It´s very important to upgrade the products in the right sequencing.

Make sure the databases has at least 50% free space

Using SQL Management Studio, you can run a simple report to make sure there are enough space available in the databases. Open up SQL Management Studio and expand databases. Right click the OperationsManager database and choose Reports->Standard Reports->Disk Usage.

This step were okay for me and i got the result below.

![](https://blog.orneling.se/assets/images/2013/11/OperationalFreeSpace.png)

Take Backups of the databases

This step is very important for being able to back if something goes wrong during the upgrade process. In my case there were already a couple of maintenance plans that i had created earlier for backing up my DB´s but I´ll go through how to take backup of the databases.

Start by right clicking the OperationsManager database and then click “Tasks” and then click “Back Up…”

Leave the default settings but change the backup path if you like to.

Click OK to execute the Back up and then go through the same procedure for the OperationsManagerDW database.

![](https://blog.orneling.se/assets/images/2013/11/Backup-DB.png)

The next step i took was making checkpoints (snapshots) of the servers included in my SCOM setup just to make it easier to back if something fails.

### The upgrade

In my case, i will have to run the upgrade process twice. My managment server holds three roles; Management Server, Operations Console and Web Console while my SQL Server holds the Operations Manager Reporting role.

The one and only option for now is of course, Install

![](https://blog.orneling.se/assets/images/2013/11/1.png)

The Management Server will be upgraded as below

![](https://blog.orneling.se/assets/images/2013/11/2.png)

 

Accept the license agreement and move on

![](https://blog.orneling.se/assets/images/2013/11/3.png)

In my case, i want to keep the location. Keep the location or change it if you like.

![](https://blog.orneling.se/assets/images/2013/11/4.png)

The Prerequisites will fail the first time in a lot of cases because of the Report Viewer Controls and the Microsoft System CLR Types for SQL Server 2012 that are required to install the Report Viewer Controls. Download these two components and then install the CLR Types followed by the Report Viewer Controls. Verify Prerequisites again and move on with the upgrade.

![](https://blog.orneling.se/assets/images/2013/11/5.png)

Stick with what you ran before the upgrade and move on.

![](https://blog.orneling.se/assets/images/2013/11/6.png)

Click Upgrade and go grab a cup of coffee (or watch the process ![:)](images/icon_smile.gif) )

![](https://blog.orneling.se/assets/images/2013/11/7.png)

After the upgrade i had to upgrade my SQL Server as well since the Reporting role were installed there. The differences in the process from the Management Server is in the following pictures.

![](https://blog.orneling.se/assets/images/2013/11/8.png)

I started the Remote Registry Service and from there i could just move on with the installation which took about 10 minutes.

![](https://blog.orneling.se/assets/images/2013/11/9.png)

### Post-Upgrade Tasks

Verify that Operations Manager now is on R2 level by opening the console and click Help and then About.

Operations Manager is now at 2012 R2 level.

![](https://blog.orneling.se/assets/images/2013/11/10.png)

Go to Administration and check the Pending Agents section where you should now see your agents. Upgrade these agents and you are good to go.

### Conclusion

The upgrade process is pretty much the same as it has been before and it´s pretty much straight forward and the upgrade process from running Windows Update to the finish line took about 2 hours.

If there´s any questions, just drop a comment below.
