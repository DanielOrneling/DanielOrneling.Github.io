---
title: "Meet the Microsoft Operations Management Suite"
date: "2015-05-08"
excerpt_separator: "<!--More-->"
categories: 
  - "azure"
  - "azure-operational-insights"
  - "microsoft-ignite"
  - "operations-management-suite"
  - "operations-manager"
  - "orneling-se"
  - "system-center-advisor"
---

This monday during the keynote of Microsoft Ignite in Chicago, Satya Nadella announced the new "Operations Management Suite" which is the new name for Azure Operational Insights. What´s new with this cloud solution other than the name is the fact that this no longer just contains log analytics and the things we´ve seen before. It is now also the place where you will manage your Azure backup jobs, Azure Site Recovery and Automation. When it comes to onboarding, it´s the exact same process as there was to onboard Azure Operational Insights (and System Center Advisor before that) and there are still two ways to connect the servers to the solution.
<!--More-->
The first method is to directly attach the server to Operations Management Suite (OMS) using the Microsoft Monitoring Agent and there is also the possibility to connect your SCOM management group to OMS as well.

**What´s new?**

The new stuff is what I mentioned above, you can now manage your Azure Backup, Automation and Azure Site Recovery inside OMS and there is much more to come. From the information I managed to get out here during the week, most of the on-prem management will be covered by the Microsoft Monitoring Agent in the future so I´m expecting to see a lot of new possibilities with this agent in the future.

Onboarding and signing in to OMS is done via [Microsoft.com/OMS](http://Microsoft.com/OMS){:target="_blank"} (quite easy to remember, huh?) and it looks like below. If you´re already signed up and using Operational Insights, all your accounts have been automatically upgraded to OMS accounts instead.

![](https://blog.orneling.se/assets/images/2015/05/050815_1525_MicrosoftOp1.png)

Once you´ve logged on to the portal, you´ll see the information about all your managed entities just like below. This brings you a great overview of what your environment looks like and the status of it so that you can be aware of new incidents and to react on those.

![](https://blog.orneling.se/assets/images/2015/05/050815_1525_MicrosoftOp2.png)

Another thing that´s gotten a new name are the Intelligence Packs known from the Azure Operational Insights days. They are now called Solutions instead and besides from the ones that came along from OpInsights, three new Solutions is available as of right now:

- Backup
- Azure Site Recovery
- Automation

With these three new features, we´ve gotten a lot more possibilities and I really think this will be great as we get one portal to manage so much more instead of running from portal to portal to do a little bit of everything everywhere. The Automation solution still requires that you switch over to the Azure portal to configure it and to create runbooks but this will soon be done from within the OMS portal as well.

![](https://blog.orneling.se/assets/images/2015/05/050815_1525_MicrosoftOp3.png)

**Wrap up**

Now, Microsoft Ignite is almost over for this time and Microsoft have packed us with new cool stuff all week so this is the first time I´ve actually managed to find some time for my blogging all week. I will do a deeper dive in OMS in the upcoming weeks to show you more of what´s new and why this is a great suite. In the meantime if you´ve got any questions, don´t hesitate to leave a comment and then I´ll get back to you as soon as possible. And of course, Ignite is still ongoing for a few more hours so if you happen to bump into me say hello and introduce yourself.
