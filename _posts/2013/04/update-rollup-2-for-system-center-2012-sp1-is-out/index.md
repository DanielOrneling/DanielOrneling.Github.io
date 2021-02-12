---
title: "Update Rollup 2 for System Center 2012 SP1 is out"
date: "2013-04-10"
categories: 
  - "app-controller"
  - "data-protection-manager"
  - "orchestrator"
  - "service-manager"
tags: 
  - "microsoft"
  - "operations-manager"
  - "system-center"
---

Yesterday, Microsoft released Update Rollup 2 for System Center 2012 SP1. This is an update covering Operations Manager, App Controller, Service Manager, Orchestrator and Data Protection Manager. As I did the last time an update was released for System Center 2012 SP1, I´m going to focus on the updates for Operations Manager alone in this post but all of the updates are available [here](http://support.microsoft.com/kb/2802159/en-us).

The updates for Operations Manager addresses the following issues, be aware that the below are just copied from Microsofts release.

**Issue 1** The Web Console performance is very poor when a view is opened for the first time.

**Issue 2** The alert links do not open in the Web Console after Service Pack 1 is applied for Operations Manager.

**Issue 3** The Distributed Applications (DA) health state is incorrect in Diagram View.

**Issue 4** The Details Widget does not display data when it is viewed by using the SharePoint webpart.

**Issue 5** The renaming of the SCOM group in Group View will not work if the user language setting is not “English (United States).”

**Issue 6** An alert description that includes multibyte UTF-8 characters is not displayed correctly in the Alert Properties view.

**Issue 7** The Chinese (Taiwan) Web Console displays the following message even after the SilverlightClientConfiguration.exe program is run:

Web Console Configuration Required.

**Issue 8** The Application Performance Monitoring (APM) to IntelliTrace conversion is broken when alerts are generated from dynamic module events such as the Unity Container.

**Issue 9** Connectivity issues to System Center services are fixed.

**Issue 10** High CPU problems are experienced in Operations Manager UI.

**Issue 11** Query processor runs out of internal resources and cannot produce a query plan when you open Dashboard views.

**Issue 12** Path details are missing for “Objects by Performance.”

### Operations Manager – UNIX and Linux Monitoring - Management Pack update (KB2828653)

**Issue 1** The Solaris agent could run out of file descriptors when many multi-version file systems (MVFS) are mounted.

**Issue 2** Logical and physical disks are not discoverable on AIX-based computers when a disk device file is contained in a subdirectory.

**Issue 3** Rules and monitors that were created by using the UNIX/Linux Shell Command templates do not contain overridable ShellCommand and Timeout parameters.

**Issue 4** Process monitors that were created by the UNIX/Linux Process Monitoring template cannot save in an existing management pack that has conflicting references to library management packs.

**Issue 5** The Linux agent cannot install on a CentOS or Oracle Linux host by using FIPS version of OpenSSL 0.9.8.

### How to install the updates

Along with an update description, there is also installation instructions and a couple of things to check out to verify that the upgrade went okay.

Install the updates using Windows Update or downloading the updates from this [link](http://support.microsoft.com/kb/2802159/en-us).
