---
title: "Update Rollup 1 for System Center 2012 SP1 is released"
date: "2013-01-09"
categories: 
  - "operations-manager"
tags: 
  - "microsoft"
  - "operations-manager"
  - "system-center"
---

Today, Microsoft released Update Rollup 1 for the System Center 2012 SP1 suite. Since this is an Operations Manager blog, I´m only listing whats new for SCOM. So what´s been fixed since the 2012 SP1 release? **Issue 1**

Agentless Exception Monitoring (AEM) in Operations Manager may provoke an increase in reporting threads and choke points.

**Issue 2**

After the Alert Attachment Management Pack (Microsoft.SystemCenter.AlertAttachment.mpb) is imported, you create a dashboard that contains an alert widget. When you click an alert, the Operations Manager console may crash.

**Issue 3**

When a Windows PowerShell module uses the Monitoringhost.exe process on an x86-based client that is running Windows 8, more than 800 megabytes (MB) of memory may be consumed.

**Issue 4**

After an application domain is created, adding another application domain may be unsuccessful.

The update can be downloaded either via Windows Update or manually via [http://catalog.update.microsoft.com/v7/site/Search.aspx?q=2784734](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=2784734) (Requires IE 6.0 and later to work properly)

Read more about the Update Rollup 1 at Microsofts site that covers the whole suite; [http://support.microsoft.com/kb/2785682](http://support.microsoft.com/kb/2785682)
