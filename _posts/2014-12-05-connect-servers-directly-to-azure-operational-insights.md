---
title: "Connect servers directly to Azure Operational Insights"
date: "2014-12-05"
excerpt_separator: "<!--More-->"
categories: 
  - "azure"
  - "azure-operational-insights"
  - "operations-manager"
  - "system-center-advisor"
---

If you´ve been around my blog for a while, you might have seen my post about how to onboard the new System Center Advisor Preview which Microsoft made available during a session at TechEd North America. What´s happened since then is that the product has got a new name, Azure Operational Insights. The product still has the same looks and functions but it better suits Microsoft´s vision of moving to Azure. Read my blog post on how to onboard System Center Advisor and connecting it to Operations Manager [here](http://www.viridisit.se/managing-system-center-opsmgr/set-new-system-center-advisor-preview/){:target="_blank"} and the post about Azure Operational Insights [here](http://www.viridisit.se/managing-system-center-opsmgr/advisor-now-azure-operational-insights/){:target="_blank"}.
<!--More-->
As I´ve already covered how to connect your on-prem Operations Manager to Operational Insights (yep, It´s the same portal) I will now you show how to directly connect a server to Operational Insights. This makes it possible to monitor logs and run assessments like malware status or software update status on our servers without the need for Operations Manager in the background. As you see in the pictures below it´s still the exact same portal but with a couple of new Intelligence Packs and a new name.

### **How to connect servers directly to Azure Operational Insights**

When you´ve created your instance and installed a couple of intelligence packs it´s time to connect our servers to the instance. This is really easy and if you´ve ever installed the Microsoft Monitoring Agent to connect to Operations Manager you will feel comfortable. Click on the "Servers and Usage" tile to get to the next step.

!![](https://blog.orneling.se/assets/images/2014/12/01.jpg)

Now that we´re in the Usage session, you will see some statistics about which intelligence packs uses the most space and the amount of servers connected. As you can see below, I´ve connected my on-prem Operations Manager management group along with one other server. Let´s give that single server a buddy by clicking Configure.

![](https://blog.orneling.se/assets/images/2014/12/02.jpg)

Here´s the parts you need to connect your server to Operational Insights. Download the agent, copy the Workspace ID and the Primary Workspace key and log on to the server you´re about to connect.

![](https://blog.orneling.se/assets/images/2014/12/03.jpg)

The following parts will be familiar for a lot of you reading this post since this is almost the same procedure as manually installing an agent and connecting it to SCOM . Launch the installer you just downloaded.

![](https://blog.orneling.se/assets/images/2014/12/04.jpg)

Choose to connect the agent to Operational Insights instead of Operations Manager.

![](https://blog.orneling.se/assets/images/2014/12/05.jpg)

Paste your Workspace ID and Workspace Key that you copied in the above step and then step through the last steps of the installation.

![](https://blog.orneling.se/assets/images/2014/12/06.jpg)

When the installation is finished, inside the Event Viewer the “Operations Manager” log have now been created. Once again, if you´ve been working with SCOM this will look familiar. As can be seen in the picture below, the online service management group have been created meaning it has been connected to Operational Insights.

![](https://blog.orneling.se/assets/images/2014/12/07.jpg)

As you can see in the picture below, I now have two servers directly connected to Operational Insights instead of just the previous one. What´s next is that the agent will report to Operational Insights which will then return the intelligence packs so the assessment can be run at the server. This might take some time so be patient and check back after a while to see your new server discovered and evaluated.

![](https://blog.orneling.se/assets/images/2014/12/08.jpg)

Now, to show that my server really have showed up in the portal I made a simple search to show all directly connected servers. The two servers below will be completely outside of Operations Manager since they are directly connected. However, if I install SQL Server for example on one of them this will show up in the portal along with some recommendations on how to configure SQL and what updates I need etc. This is of course depending on me activating the SQL Server intelligence pack.

![](https://blog.orneling.se/assets/images/2014/12/09.jpg)

### **Working with the information provided**

Below you will see what I´ve done to “My dashboard”. I´ve included the information I´m interested in for the moment and the tiles can be configured to include thresholds. One example is “Missing Security Updates” which spans over all the lab environment and it alerts when the value is above 80. When I click on the tile, I´ll get a good summary of what updates are missing and on which server. Below values is only based on the last 7 days but it can be changed to whatever time frame you want as long as there´s data inside Operational Insights to suit your demands.

![](https://blog.orneling.se/assets/images/2014/12/10.jpg)

### **Wrap Up**

What I´ve shown above is how to connect a server to Operational Insights directly but also how to get an assessment of what software updates is missing in the environment for example. This is great information as it points us in the right direction and we´ll know what server to go to first and what updates to install. If you´re not on Operations Manager today, this might be a good start to get an overview of your environment and it will provide you with some tips on how to configure your databases according to best practice among many other things. If there are any questions, don´t hesitate to leave a comment below.
