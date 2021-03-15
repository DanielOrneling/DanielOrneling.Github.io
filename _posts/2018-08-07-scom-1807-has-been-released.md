---
title: "SCOM 1807 has been released"
date: "2018-08-07"
excerpt_separator: "<!--More-->"
categories: 
  - "operations-manager"
  - "orneling-se"
---

So, the summer is almost over and I´m back from my vacation. In other words, time to dig into things again. A couple of weeks ago Microsoft launched System Center 1807 as an update for the previous version, 1801. So let us dig into SCOM 1807.

When System Center 1801 was launched, it marked the start of the Semi-Annual Channel which means that a new version will be released twice a year. You can read more about the different release models in my blog post [here](https://blog.orneling.se/2017/11/news-about-scom-1801){:target="_blank"}.
<!--More-->
**So what´s new in SCOM 1807 then?** There are some nice additions in this new version as you can see below;

**Configure APM component during agent install or repair** With this new possibility, we get to choose whether APM should be enabled for the agent or not. This was a problem with earlier agents (2016 and 1801) that could cause a crash with IIS Application Pools. This could also lead to a crashing SharePoint Central Administration application pool running .Net Framework 2.0. Now you can enable or disable APM for an agent either during installation or a repair of the agent.

**Web console enhancements**

- A new PowerShell widget has been added
- An effective configuration widget in the Monitoring objects detail page has been added that shows the running rules and monitors and what override settings have been applied
- Alert widget enhancement includes an improved layout and presentation of alert details. You´re able to modify the resolution state and drill down to the Monitoring object details page for the alert source.
- The monitoring tree can be hidden when a dashboard is integrated with SharePoint.
- You can change the size of the health icon in the Topology widget.
- You can now manage maintenance schedules in the web console, the same you would do it in the Operations Console
- People who have been assigned the “User” and “Operator” roles can now create dashboards in My Workspace.
- Network node/network interface drill-down is now available as a tab when you select a network device and drill-down to the Monitoring objects detailed page. It delivers the same experience as what is available in the Operations console.

![](https://blog.orneling.se/assets/images/2018/08/scom_1807_release_1.png)

![](https://blog.orneling.se/assets/images/2018/08/scom_1807_release_2.png)

**Support for SQL Server 2017** Now you can upgrade the SQL platform for SCOM from SQL Server 2016 to SQL Server 2017.

**Operations Manager and Service Manager console coexistence** The Operations and Service Manager version 1807 consoles, as well as PowerShell modules can be installed on the same system. (Thank you very much for this one!)

**Linux log rotation** To prevent the SCX logs from growing and consuming all available free space on the system disk, a log rotation feature is now available for the SCX agent.

**Support for OpenSSL 1.1.0** The support for OpenSSL 0.9.8 has been dropped and support for OpenSSL 1.1.0 has been added

**Support for Ubuntu 18 and Debian 9** These platforms are now available for monitoring using a SCOM agent

**Auto detection of Pseudo FS and drop Enumeration.** The UNIX and Linux agent has been enhanced to detect pseudo file system dynamically and ignore enumeration.

**How do I upgrade from SCOM 1801 to SCOM 1807?** I would really love to make a separate post about the upgrade process, but it´s really easy to get going. If you ever applied an Update Rollup to your SCOM environment, you will have an aha moment.

Check [this link](https://docs.microsoft.com/en-us/system-center/scom/upgrade-1801-to-1807?view=sc-om-1807){:target="_blank"} out to see how you can apply the update.

**Summary**

This was the news in SCOM 1807 which I think adds a lot of value. I will continue working with 1807 so stay tuned for more information here on the blog.

As always, if you have any questions don´t hesitate to contact me. Just leave a comment below and I´ll get back as soon as possible.