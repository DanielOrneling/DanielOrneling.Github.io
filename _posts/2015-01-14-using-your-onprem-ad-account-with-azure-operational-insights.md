---
title: "Using your onprem AD account with Azure Operational Insights"
date: "2015-01-14"
excerpt_separator: "<!--More-->"
categories: 
  - "azure"
  - "azure-operational-insights"
  - "orneling-se"
---

Besides from moving my blog to my own again, I´m also broadening the scope of what I´m going to write about from only covering Operations Manager which will still be the main focus to also cover things like Azure Operational Insights and other parts of System Center and Azure as well.
<!--More-->
As a step towards more focus on Azure and the future for a lot of products, I recently passed the 70-533 certificate “Implementing Microsoft Azure Infrastructure Solutions” which some of you might be familiar to if you attended the 4-day on-line course in the beginning of December 2014. If you have no idea what I´m talking about and you think it sounds interesting, visit Channel 9 [here](http://channel9.msdn.com/Events/Microsoft-Azure/Level-Up-Azure-IaaS-for-IT-Pros){:target="_blank"} to find the recorded sessions and you will then have come a long way towards passing the above mentioned exam :).

As you might have seen before, I´ve already covered Azure Operational Insights (former System Center Advisor) in a few posts and now that It´s setup I wanted to be able to logon using my On-prem AD accounts instead of my Microsoft account. Below, I will go through the process of adding your organization and being able to log on using your AD account from the Azure Operational Insights portal. This however requires you to first set up Azure AD Sync before this is possible. In my case I´ve set up Azure AD Sync and AD FS so in my case, I´m using Single Sign On to access my Operational Insights subscriptions.

**Connecting the organization to allow access to Azure Operational Insights**

So, how is this done? After logging in to the OpsInsights portal with an account that also has access to the Azure subscription, click the gearwheel at the top and you´ll find yourself in the Settings section.

![](https://blog.orneling.se/assets/images/2015/01/1.jpg)

Click ”Add organization” and then step through the following process. Choose to log in with an organizational account.

![](https://blog.orneling.se/assets/images/2015/01/2.jpg)

![](https://blog.orneling.se/assets/images/2015/01/3.jpg)

When you get to this page, in this case my own ADFS site logon using the format DOMAIN\\User and then Sign in.

![](https://blog.orneling.se/assets/images/2015/01/4.jpg)

Grant access for the user to the OpsInsights subscription and you have created yourself a new administrator.

![](https://blog.orneling.se/assets/images/2015/01/5.jpg)

Now when the user you used to log on has become an administrator, It´s time to click “Manage Users” to allow more users to access the data gathered by Operational Insights.

![](https://blog.orneling.se/assets/images/2015/01/6.jpg)

To add a user, click Add and then choose Organizational account. Choose whether you want to add a single user or a group, type the name (or just click the look it up button to show all possible users) and look it up to make sure it´s the correct user/group and then choose which Workspace role you´d like. Finish with OK and you will then have a couple more users.

![](https://blog.orneling.se/assets/images/2015/01/7.jpg)

This shows how easy it is to allow your organizational users to access Operational Insights once you have the Azure AD part configured. A huge benefit of this is that your users now only need to sign in the first time accessing the portal and in my case, I don´t have to log on each time I want to check out OpsInsights.

**Wrap up**

Of course, this only shows a real tiny bit of what you can do using the different roles of Azure but still, it makes life a bit easier for our staff when they can use their AD accounts in more places instead of needing a lot of other logins. From now on you will see more of Azure in my posts, both combined with Operations Manager for example but also stand-alone Azure posts. I really hope you enjoy visiting my new blog and as always, the comment field is all yours :).
