---
title: "Operations Manager 2012 R2 Update Rollup 1 is available"
date: "2014-01-29"
excerpt_separator: "<!--More-->"
categories: 
  - "operations-manager"
---

And so the time has come for the first Update Rollup to be released for System Center 2012 R2. The Update Rollup 1 is available for the whole System Center suite but since I´m focusing on Operations Manager, this is the product i will concentrate on. Update Rollup 1 for the other components can be found [here](http://support.microsoft.com/kb/2904734){:target="_blank"}.
<!--More-->
### Operations Manager

The update for Operations Manager takes care of the following issues:

- **Issue 1**
- An error occurs when you run the **p\_DataPurging** stored procedure. This error occurs when the query processor runs out of internal resources and cannot produce a query plan.

- **Issue 2**
- Data warehouse **BULK INSERT** commands use an unchangeable, default 30-second time-out value that may cause query time-outs.

- **Issue 3**
- Many 26319 errors are generated when you use the Operator role. This issue causes performance problems.

- **Issue 4**
- The diagram component does not publish location information in the component state

- **Issue 5**
- Renaming a group works correctly on the console. However, the old name of the group appears when you try to override a monitor or scope a view based on group.

- **Issue 6**
- SCOM synchronization is not supported in the localized versions of Team Foundation Server.

- **Issue 7**
- An SDK process deadlock causes the Exchange correlation engine to fail.

- **Issue 8**
- The "Microsoft System Center Advisor monitoring server" reserved group is visible in a computer or group search.

- **Issue 9**
- Multiple Advisor Connector are discovered for the same physical computer when the computer hosts a cluster.

- **Issue 10**
- A Dashboard exception occurs if the criteria that are used for a query include an invalid character or keyword.

### Operations Manager - UNIX and Linux Monitoring (Management Pack Update)

Below are the updates for the Operations Manager - UNIX and Linux Monitoring (Management Pack Update) listed:

- **Issue 1**
- On a Solaris-based computer, an error message that resembles the following is logged in the Operations Manager log. This issue occurs if a Solaris-based computer that has many monitored resources runs out of file descriptors and does not monitor the resources. Monitored resources may include file systems, physical disks, and network adapters.

- **Note** The Operations Manager log is located at /var/opt/microsoft/scx/log/scx.log.errno = 24 (Too many open files)
- This issue occurs because the default user limit on Solaris is too low to allocate a sufficient number of file descriptors. After the rollup update is installed, the updated agent overrides the default user limit by using a user limit for the agent process of 1,024.

- **Issue 2**
- If Linux Container (cgroup) entries in the /etc/mtab path on a monitored Linux-based computer begin with the "cgroup" string, a warning that resembles the following is logged in the agent log.
- **Note** When this issue occurs, some physical disks may not be discovered as expected.
- Warning \[scx.core.common.pal.system.disk.diskdepend:418:29352:139684846989056\] Did not find key 'cgroup' in proc\_disk\_stats map, device name was 'cgroup'.

- **Issue 3**
- Physical disk configurations that cannot be monitored, or failures in physical disk monitoring, cause failures in system monitoring on UNIX and Linux computers. When this issue occurs, logical disk instances are not discovered by Operations Manager for a monitored UNIX-based or Linux-based computer.

- **Issue 4**
- A monitored Solaris zone that is configured to use dynamic CPU allocation with dynamic resource pools may log errors in the agent logs as CPUs are removed from the zone and do not identify the CPUs currently in the system. In rare cases, the agent on a Solaris zone with dynamic CPU allocation may hang during routine monitoring.
- **Note** This issue applies to any monitored Solaris zones that are configured to use dynamic resource pools and a "dedicated-cpu" configuration that involves a range of CPUs.

- **Issue 5**
- An error that resembles the following is generated on Solaris 9-based computers when the /opt/microsoft/scx/bin/tools/setup.sh script does not set the library pathcorrectly. When this issue occurs, the omicli tool cannot run.
- ld.so.1: omicli: fatal: libssl.so.0.9.7: open failed: No such file or directory

- **Issue 6**
- If the agent does not retrieve process arguments from the getargs subroutine on an AIX-based computer, the monitored daemons may be reported incorrectly as offline. An error message that resembles the following is logged in the agent log:
- Calling getargs() returned an error

- **Issue 7**
- The agent on AIX-based computers considers all file cache to be available memory and does not treat minperm cache as used memory. After this update rollup is installed, available memory on AIX-based computer is calculated as: free memory + (cache – minperm).

- **Issue 8**
- The Universal Linux agent is not installed on Linux computers that have OpenSSL versions greater than 1.0.0 if the library file libssl.so.1.0.0 does not exist. An error message that resembles the following is logged:
- /opt/microsoft/scx/bin/tools/.scxsslconfig: error while loading shared libraries: libssl.so.1.0.0: cannot open shared object file: No such file or directory

You can find the original article [here](http://support.microsoft.com/kb/2904678){:target="_blank"}.

### How to install the update

You will find the update ready for download [here](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=2904678){:target="_blank"} at the Windows Update Catalog.

The install instructions can be found [here](http://support.microsoft.com/kb/2904678){:target="_blank"} under the "Installation Instructions" chapter.

 

Any questions? Leave a comment below.
