---
title: "Azure Governance – What´s that and why should I care?"
date: "2019-11-08"
excerpt_separator: "<!--More-->"
categories: 
  - "automation"
  - "azure"
  - "azure-monitor"
  - "log-analytics"
  - "microsoft-ignite"
  - "orneling-se"
---

Ever since Azure was a new thing and before it “went live”, we´ve been fed with how easy it is to get started using different services. One of my first experiences were when I deployed my blog on to the Azure platform somewhere back in 2012, and I was up and running in literally less than fifteen minutes, and this was the first time I did it which is why it took that long a time. It was just as simple as picking a Wordpress instance from the gallery and deploying it. A similar experience was when I deployed my first virtual machine. A few clicks and a short time for the deployment and I had my new virtual machine ready to connect to.
<!--More-->
#### The evolution of Azure

Sure, that was easy and something anyone could do, but was it the right way? Since 2012 when these events occurred, a lot has happened with Azure, and I really mean a lot! The most important change is that we´ve gone from Azure “Classic” to Azure Resource Manager (ARM), where the first generation of Azure were built upon XML, while the second generation is built upon JSON. That and a lot of other possibilities, such as the use of Rescource Groups make it more complex, but at the same time a more mature and safer experience using Azure. The right way to deploy new resources nowadays is to use ARM templates, which is a JSON formatted template telling what to deploy and how to configure it. The advantage of this is that every time you´re deploying something using the template it will be deployed the exact same way, eliminating the human factor.

#### **The easy way vs. the right way**

I´ve mentioned how easy it is to get started, but does that mean it’s the right way to do it? Nope, not necessarily. Just as were used to from our on-prem environments, there´s this thing called best-practice to take into consideration. More possibilities also mean we must think our deployments through a lot more. I mentioned resource groups earlier which gives us the ability to split our deployments into several different resource groups, all which can be provided with their own sets of rights assignments.

While we deploy more and more resources, there are another huge thing to remember, Azure Governance, which lets us control our Azure based environment using policies to control how it´s being both deployed but also managed.

#### Azure Governance - The right way

Azure governance consists of three mayor areas, Management Groups, Policies and Blueprints (more about this in a later post). Just as we have Group Policy on-prem, this is our way of controlling the environment in the cloud. Management Groups let us group several different subscriptions to make it able to mirror the organization. For example, you can assign one subscription to the HR department, and others for the dev team such as a Dev and Staging environment. This makes it easy to follow up on which parts of the organization spends the most money, but that’s not the only advantage this bring. We can also assign policies subscription-wide and use access control based on our preferences.

With policies comes the ability to control how the environment should behave and if we have any requirements about how a resource should be equipped.

Below are just a few already made policies which involves virtual machines. Should you not find anything of your liking, you can always create your own policies.

![](https://blog.orneling.se/assets/images/2019/11/governance-1.jpg)

#### **Azure Policy – The way to keep the control**

With Azure Policy we can assign several policies and we can choose if they should just be auditing or forcing. The difference is that a policy that audits does nothing with the resource, it just audits and reports it back for us to know about, while a forcing policy actively denies certain configurations or won’t let you continue until certain requirements are met.

A few examples of what a policy can achieve:

- Enforce the use of tags for our resources making some tags mandatory, such as cost place, business unit or environment
- Specifying which VM sizes can be used when deploying new servers
- Allowing certain regions only for resources to be deployed (extra useful when the company spans over different countries or continents)
- Enforcing a naming policy
- Installing an extension to all new servers, connecting it to Azure Monitor for example

#### **Enforcing a monitoring policy to all servers**

The last example mentioned above is something I want to spend some more time elaborating. We´re (hopefully) already used to monitoring our on-prem environment using System Center Operations Manager for example, but most often this tool isn’t used to monitor cloud resources other than IaaS VM´s from time to time, but now we need to be monitoring our cloud resources as well to keep the environment safe and running.

To make sure our resources are being monitored we can assign a policy that forces the installation of the Log Analytics monitoring agent for all servers that are deployed in the subscription. This can be configured to take effect subscription-wide or for certain resource groups only. This means that if a user deploys a server from an ARM template that don’t include the Log Analytics agent extension, this will be automatically deployed afterwards, ensuring our resources are being monitored the way we intend to, in a certain workspace.

I assigned this policy to my subscription, deployed two servers as seen below, "EU-SE-VM0001" and "NA-US-VM0001" and in about twenty minutes they had the Log Analytics agent installed, just as intended.

![](https://blog.orneling.se/assets/images/2019/11/governance-2.jpg)

And just to verify that the servers are communicating with Azure Monitor (of which Log Analytics is a part) I ran this simple query seen below to collect the information about the server’s heartbeats and their IP address along with the country they are deployed.

![](https://blog.orneling.se/assets/images/2019/11/governance-3.jpg)

Yes, the SE VM is based in Ireland but that´ll change once the Azure datacenter in Sweden opens.

#### Learn more about Azure Monitor in these posts:

- [Get notified on Azure service health issues](https://blog.orneling.se/2019/06/get-notified-on-azure-service-health-issues){:target="_blank"}
- [Looking at the available Azure Monitor data sources](https://blog.orneling.se/2019/06/looking-at-the-available-azure-monitor-data-sources){:target="_blank"}
- [Azure Monitor – Getting started with alerting](https://blog.orneling.se/2019/05/azure-monitor-getting-started-with-alerting){:target="_blank"}
- [Migrating lots of agents to Azure Log Analytics](https://blog.orneling.se/2019/05/migrating-lots-of-agents-to-azure-log-analytics){:target="_blank"}

#### **So how can I Azure Governance in my environment?**

There´s no short answer to that. You can either use a single policy or multiple policies, where the latter is the recommendation to make sure you take good care of your resources. Earlier this week during Microsoft Ignite in Orlando, Microsoft announced Azure ARC which is a tool that you can use to manage all your resources “the Azure way” no matter where they´re deployed. This means that even if your resource is deployed in AWS, Google Cloud or on-prem, you can still use ARM templates and policies like the one above installing agents for those resources. Azure ARC is still the new kid on the block, but I have a feeling we will hear a lot about it soon and I´m pretty sure it will come to great use.

It also helps big time in controlling the environment and keeping it safe even with those resources that aren´t deployed in Azure, and we can keep control of them in one place instead of several different portals and tools.

If you want to read more about Azure ARC, you can do so [here](https://azure.microsoft.com/en-us/services/azure-arc/){:target="_blank"}.

#### **Summary**

With this post I have started scraping the surface when it comes to Azure Governance and I´m no way near showing it all off since there’s really a lot to show in this area. It´s really important to invest in this area since it´s about securing our cloud resources, especially when more and more investments are being made in the cloud. With all the new resources being deployed, there´s a bigger need for tagging and RBAC (access control) etc. and all that can be pretty easily controlled using policies and placing them in different management groups.

I will keep digging in to this area of Azure Governance and instead of doing one mayor post I´ll write several covering different scenarios instead so keep your eyes open if you think this seems interesting.

If you have any questions, leave a comment below and I´ll get back to you.
