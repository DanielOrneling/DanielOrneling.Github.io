---
title: "SCOM 1801 has been relased"
date: "2018-02-09"
categories: 
  - "operations-management-suite"
  - "operations-manager"
  - "orneling-se"
---

Yesterday the news finally came, System Center 1801 has been relased. An with that, of course SCOM 1801.

This is the first release in the new Semi-Annual Channel which will release twice a year while the Long-Term Servicing Channel will be released at a much lower cadence.

**But what´s the difference between these two tracks?** The Semi-Annual Channel

- You will receive the latest updates and features with releases twice a year
- Each build (1801,1807 etc.) is supported for 18 months, then you must move to a newer build
- New features added (all the new features will be put into this channel)

The Long-Term Servicing Channel

- You will receive new versions at a much slower pace (think SCOM 2012 and SCOM 2016 as an example)
- 5 years of mainstream support and 5 years of extended support
- Update Rollups only, mostly fixes and probably around zero new features added

**So what´s new in SCOM 1801 then?** The list of news;

- **Enhancements in performance** that for example allow for the console to continue to respond while a management pack is imported, deleted or changed. ”Updates and Recommendations” that were launched with SCOM 2016 now includes third-party products based on customer feedback.
- **Log file monitoring for Linux/UNIX servers**. With the support for FluentD you can now monitor Linux/Unix logs just as well as you can monitor Windows server logs. Some of the news is that you can now use wildcards in the log names and directories.
- **Added support for Kerberos authentication between management servers and Linux/Unix servers.** This adds to the security since you no longer need to activate ”basic authentication” for Windows Remote Management (WinRM).
- **Integration between Operations Manager and Service Map**, which is a part of Operations Management Suite (OMS). This integration gives you the ability to automatically map your applications and have distributed applications automatically generated (and maintained) in SCOM.
- **Support for installing SCOM on Windows Server 1709**. Note that 1709 is Core-only. There is no GUI available in this version, instead you should be looking at “Project Honolulu” for remote management.
- **A completely new way of upgrading SCOM** to newer versions (YY/MM) directly from within the Operations Console.
- And last, but not in any way the least. **A completely re-rebuilt all HTML5 web console** with no dependencies to Silverlight! (Finally!) You can now create your own dashboards inside the web console stored in a management pack of your choice, which makes it easy to export and backup those dashboards to be re-used. This new console will work in several different web browsers since there are no Silverlight dependencies. See an example below.

**How can I upgrade to SCOM 1801?** 1801 supports an in-place upgrade from the following versions:

- System Center 2012 R2 UR12 to the latest update rollup
- System Center 2016 RTM to the latest update rollup

**Update:** It seems there was a typo in the documentation when I originally wrote this post saying that 2012 R2 RTM could be upgraded to 1801. That´s wrong, you MUST be at least on UR12 to be able to upgrade to 1801.

**Summary** I will check more into this new release in the near feature as I already have a number of posts planned about it. In the meantime, if you have any questions, just add a comment below and I´ll get back as soon as possible.

[![](images/system_center_operations_manager_replacement_icon_by_flakshack-d5mxgid.png)](http://media.orneling.se/2018/02/system_center_operations_manager_replacement_icon_by_flakshack-d5mxgid.png)
