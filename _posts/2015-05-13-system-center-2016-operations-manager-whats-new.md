---
title: "System Center 2016 Operations Manager - What´s new"
date: "2015-05-13"
excerpt_separator: "<!--More-->"
categories: 
  - "dashboards"
  - "live-maps"
  - "management-packs"
  - "microsoft-ignite"
  - "operations-management-suite"
  - "operations-manager"
  - "orneling-se"
---

So as i mentioned in my last post, I was one of the lucky 23.000 persons who got to attend Microsoft Ignite in Chicago where IT professionals, exhibitors and Microsoft came together in a large conference to share all the news and to meet new people. Since I´m a SCOM fanatic and have been for a long time, I want to share some of the news that came up during the week on what we can expect from System Center 2016 Operations Manager. Below is just a summary of what´s to come, I will evaluate the news in upcoming posts to give you a hint on what to expect.
<!--More-->
- Nano Server Management Pack
    - The new Nano version of Windows Server is a version that´s been put on a heavy diet and the only way to administer this version is by Win RM or Powershell. Of course, this server version couldn´t be monitored by the regular MP for Windows Server meaning we are looking at a coming MP just for this version.
- New version of the Microsoft Monitoring Agent to fit the Nano server
    - The Nano server will also receive a new version of the Microsoft Monitoring Agent to make sure it will run on that version as well as the regular versions of Windows Server.

- New dashboards just as in the SQL Server 2014 Management Pack
    - The dashboards that were launched along with the SQL Server 2014 Management Pack turned out to be so popular that it will be made generally available. This means that we will be able to include our IIS Servers, SQL Servers, Performance counters and so on in this faboulous dashboard. See the picture below for an example (I know my cell camera is kind of crappy :).
    - ![](https://blog.orneling.se/assets/images/2015/05/IMG_20150508_130859.jpg)
- Scheduled maintenance mode from within the console
    - One of the things that really is missing so far in the Operations Console is a method to plan upcoming maintenance mode. This have of course been possible to do but then it has to be done by PowerShell (see my blog post [Schedule Operations Manager maintenance mode](https://blog.orneling.se/2014/01/schedule-operations-manager-maintenance-mode){:target="_blank"} for my recommendation on how to do it). This will be taken care of with a new wizard that you can launch from the Operations Console and to make sure that you don´t need any PowerShell scripts to make it happen. As it sounded during the session, this will be delievered to SCOM 2012 R2 as well via an Update Rollup sometime in the summer or fall.
- New Management Packs for Server 2016
    - As the Windows Server 2016 is released, a lot of new management packs are under developement to make sure we can monitor all those roles and features we will be using in the future running on Server 2016. The MP´s they´ve mentioned so far can be seen in the picture below.
    - ![](https://blog.orneling.se/assets/images/2015/05/IMG_20150508_124853.jpg)
- New Azure MP
    - If you like me have been monitoring your Azure services using SCOM, you would know that there is a quite long process in order to get started. In the current version you need a self signed management certificate, upload it to Azure and then import it into SCOM. This is not the case with the upcoming new version which will be launched sometime during this summer. Find out more about this as soon as I can lay my hands on it.
- The MP catalog is having a make-over
    - As of today the MP catalog inside Operations Console only contains a few new management packs meaning you will need to go online to find the latest versions. This will be taken care of and the MP catalog will have a make-over to make sure the MP´s will be made available from within the console.
- Install preferred partner solutions from the console
    - When it comes to System Center, there´s a lot of partner solutions available out there like [Savision](http://www.savision.com){:target="_blank"} Live Maps and Dashboards, [Squared Up](http://www.squaredup.com){:target="_blank"} and so on which all adds an extra value to SCOM in this case. As there are a lot of solutions out there, Microsoft wants to bring those solutions to us so we will be able to install trial versions of these solutions from the console. Right now, I don´t know how this will work or look as I haven´t seen it in action but you can count on me to get back to it once I get the chance to dig into it :)
- Integration into Operations Management Suite
    - As we´ve alread seen, SCOM will be able to connect to [Operations Management Suite](http://www.Microsoft.com/OMS){:target="_blank"} just as it has been done up until today with Azure Operational Insights.

What you´ve seen here is the key takeaways from Microsoft Ignite concerning SCOM and what´s to come in the 2016 version. If you like what you see in this post and want to see more of it, keep your eyes open cause "someone" told me several new posts are coming which are focusing on these new possibilites :)

Have any questions? Drop a comment below!
