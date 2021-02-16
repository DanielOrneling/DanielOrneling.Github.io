---
title: "Monitoring the VMware environment – Part 1"
date: "2018-09-27"
excerpt_separator: "<!--More-->"
categories: 
  - "azure"
  - "log-analytics"
  - "management-packs"
  - "operations-manager"
  - "orneling-se"
  - "vmware"
---

Lately I have been working a lot with monitoring VMware using SCOM for some of our largest customers and have gotten to think about this more and more. Even though cloud providers such as Amazon Web Services (AWS) and Microsoft Azure keeps on showing great numbers of growth (and profits for that matter), the absolute majority of customers IT are still on-prem. Since about ten years, virtualization has been about the coolest thing there is and the largest player in this area is still VMware.
<!--More-->
Thinking about how large this area is and the importance for the organization, we need to monitor the VMware platform. Just as well as we need to keep track of what’s happening with our services, such as web shops or other business critical systems, we need to monitor the foundation it all relies on as well.

### **Start looking at Veeam and OpsLogix**

Since I started looking into VMware monitoring some years back, I have gone with Veeam who has been the larger player in this field historically and may have been the first choice for many. At first, I wasn’t really aware of any other competitor and Veeam had really done a good job but then I started exploring other possible solutions as well. The other player I´m talking about is OpsLogix who have been developing their VMware management pack as well for some years now. It has happened a lot during the years, not just speaking of pricing but also in terms of functionality. Hence, this post series.

One of the first thing I noticed when I started working with Veeam and their management pack was the amount of documentation and dashboards available. This is something that really stands out when looking into VMware monitoring.

So, then I started looking at OpsLogix´s solution as well, and the first thing that hit me was that there wasn´t as much documentation. At first this felt odd, but then I started working with it and now I have a lot more experience, both from working with the management pack but also in the area of VMware monitoring itself.

### **The interview**

For this blog post series, I have decided to contact both players to get to know about their visions, their experiences and their thoughts about the future.

So far, I have managed to speak to Vincent de Vries who is the director at OpsLogix. Find the interview below;

#### _Why did you start developing your own VMware Management Pack while there where already other packs out there?_

_In 2013 we saw that there were two major players in the market which offered a commercial VMware Management Pack. One was, in our opinion, overpriced although it contained a lot of nice features. The other was, well let’s say, not the most stable and easy to configure (former Bridgeways). With our Management Pack authoring experience, and specially our experience building managed modules for SCOM, we felt that we could develop a management pack which would have a less of a performance footprint, with good stability and far more competitively priced._

_We’re happy to say that, in the same year, a few institutes with very large VMware environments got involved fully supporting our endeavor!_

#### _What were the difficulties you had to overcome developing the VMware Management Pack_

_Getting data from VMware through the vSphere API and making it play nice with SCOM modules. In the end our team spent countless hours exploring the vSphere API and writing code to translate the VMware metrics to a format that SCOM could work with. Also handling very large amounts of data in SCOM is a challenge, so in the first version we used all the SCOM optimization tricks we could think of._

#### _Is your VMware Management Pack ready for the latest version of SCOM?_

_Yes! We have tested our VMware Management Pack on SCOM 1801 and found that it works seamlessly with the latest version of SCOM._

#### _Is your VMware Management Pack compatible with the latest version of vSphere?_

_Yes, we tested it on vSphere 6.7, and we will continue to test it whenever new versions of vSphere are released._

#### _How Does your VMware Management Pack collect information from VMware?_

_We use two methods:_

1. _By querying the vSphere API. Although the vSphere API is rather complex, the information you get from it on your VMware environment is very complete, so it is great for monitoring._
2. _By querying the ESXi host directly, this can be done in a similar way as querying the vSphere API, only you have slightly less information available._

#### _How well does your MP scale for large enterprises?_

_The current version we are running scales very well in enterprise environments, the bottleneck is usually a SCOM sizing related issue when we do run into performance issues. In the new redesigned version that we are currently testing, we have made a huge investment in lowering the performance footprint for SCOM. The test results are very promising, which show that it can handle monitoring of 400-800 ESXi hosts without issue__._

#### _Will your VMware Management Pack ever be usable in Azure?_

_Yes, fortunately our VMware Management Pack is designed in such a way that little effort is required to get it to collect of OMS or Log Analytics._

#### _What is the performance impact on SCOM?_

_That depends on the size of your VMware environment, and whether you want to monitor server hardware, enable in depth monitoring for ESX hosts, monitor all VM’s etc. Like every other Management Pack, our VMware Management Pack starts up workflows for every monitor and rule, but unlike the other Management Packs we painstakingly made sure that all the workflows are optimized to minimize resource consumption in SCOM.  In general, I have to say that we are very happy with the performance of our VMware Management Pack, but we always think we can improve and continually look for performance gains._

#### _Now that cloud computing is growing and on-prem shrinking, are you still investing in the VMware MP?_

_Absolutely. We believe that Azure, and cloud computing in general, will continue to win ground, but we also believe that an equilibrium with be reached at some point between cloud and on-prem computing. There are plenty of reasons why companies still choose to have a large part of their IT environment on-prem, so for the foreseeable future we see plenty of reason to keep investing in our VMware Management Pack._

#### _If you are continuing to put resources toward developing the VMware Management Pack, what features are you developing?_

_Our goal is to offer a VMware Management Pack with the least performance impact and with the most useful information for (VMware) admins. We already provide great looking dashboards in SCOM, visualizing your VMware environment, so when we talk about new features we tend to talk about how to improve the current feature set. In our experience, admins are not interested in ever more new features, instead they are more interested in quality information and relevant alerting on their VMware environment._

[](https://blog.orneling.se/assets/images/2018/09/1.jpg) 
Some of the performance data you can look at in the Operations console. Click for a larger image.

[](https://blog.orneling.se/assets/images/2018/09/2.jpg) 
Here we can see the status of the fans in the hardware being monitored by the management pack. Click for a larger image.

[](https://blog.orneling.se/assets/images/2018/09/3.jpg) 
This is what it may look like, using OpsLogix´s solution in Azure Log Analytics to send information about how the VMware is behaving. Click for a larger image.

### **Summary**

That’s a wrap-up for the first post of this series where I go deeper in the VMware monitoring field, especially looking into OpsLogix´s management pack. As you can see, there´s a lot to it and it’s a big thing just covering VMware monitoring. In the next post I will look at Veeam´s management pack for VMware and dig deeper, just as I´ve done for this blog post. Stay tuned for the coming posts, it will be worth your while.