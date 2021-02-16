---
title: "Set up Operations Manager AD Integration"
date: "2013-11-27"
excerpt_separator: "<!--More-->"
categories: 
  - "operations-manager"
---

In this post i will guide you in how to integrate Operations Manager with the AD to automate the agent assignment process. The easiest way to deploy agents is of course via the Operations Console, but is this always the right way to do it? No, not always. If your using SDI and NAP for example where the windows firewall are heavily used, deployment from the console is not the right way to do it. One of the solutions that I will go through in this post is the AD integration which is quite easy to implement and it keeps the firewall ports needed for SCOM down to a minimum.
<!--More-->
### What is it and what does it mean?
The whole idea with AD integration is that when an agent is manually installed, for example using GPO or System Center Configuration Manager it should automatically find which Management Group it belongs to and what Management Server it should be talking to. This is possible by creating a container in the AD that contains information about Management Group name and Management Servers that are in the Management Group. After the container has been created, a rule must be created for the Management Server as well that says which servers should talk to which Management Server.

### Creating the container

On your Managment Server, locate the install media and navigate to SupportToolsAMD64. Either copy the file MomADAdmin.exe or run it directly from there.

Open an elevated command prompt and run the following command; (my command will follow as an example. Make sure your admins group is in the format _domainsecurity\_group_, otherwise it will not work.

```
MOMADAdmin.exe <ManagementGroupName> <MOMAdminSecurityGroup> <RunAsAccount> <Domain>
```

```
MOMADAdmin.exe ORNELING ORNELINGScom_Admins scomaction_svc ORNELING
```

Executing this command must be done by an account with Domain Admins right to be able to create the container. See below how it´s done;

![](https://blog.orneling.se/assets/images/2013/11/1.jpg)

 

Here´s how the AD looks after the command had been executed.

![](https://blog.orneling.se/assets/images/2013/11/2.jpg)

### Configure the Management Server to allow new agents to communicate with it

The next thing after the container has been created is to configure the Management Server with a rule that allows new installed agent to communicate with it.

This is done by navigating in the console to Administration -> Management Servers and right clicking the server you want to configure. See the pictures below and follow the process.

![](https://blog.orneling.se/assets/images/2013/11/3.jpg)

 

Click Next to move on with the wizard

![](https://blog.orneling.se/assets/images/2013/11/4.jpg)

 

Click "Configure..." to start creating your AD query.

![](https://blog.orneling.se/assets/images/2013/11/5.jpg)

 

Create a query that matches your needs, in my case my servers are all named TBOM etc. so i want the name to start with TB to be picked up by this rule.

![](https://blog.orneling.se/assets/images/2013/11/6.jpg)

 

If there are servers that should´nt be picked up by this rule, type in the FQDN of them here to exclude them from the rule.

![](https://blog.orneling.se/assets/images/2013/11/7.jpg)

 

Create your failover rules if you don´t want Automatic failover to happen. In this case, i only have one Management Server so I´m sticking to the default value.

![](https://blog.orneling.se/assets/images/2013/11/8.jpg)

 

The next thing was to Delete the Management Group Data on one of my agent machines to test the rule. I opened up Microsoft Monitoring Agent from the Control Panel and deleted the information. After "Automatically update management group assignments from AD DS" has been checked, press Apply and then wait for a while for the AD rule to run.

![](https://blog.orneling.se/assets/images/2013/11/9.jpg)

 

After a while you can see this event in the Operations Manager event log on the Management Server. As you can see, six servers matched my criteria and were added to the AD group.

![](https://blog.orneling.se/assets/images/2013/11/10.jpg)

 

After the event seen above, the agent information had been updated on my agent server and it started answering to heart beats again.

![](https://blog.orneling.se/assets/images/2013/11/11.jpg)

 

### Conclusion

So, now you´ve seen how the AD integration is done in Operations Manager, it works the same way in at least SCOM 2012, 2012 SP1 and 2012 R2 so there is´nt any news in how to implement it since SP1. This can be used in small and large environments, it all depends on the needs for the organization. Some customers deploy the agents from the console while others want to deploy it using SCCM. This method only demands that the TCP 5723 port is opened for SCOM other than the ports needed for SCCM etc.

If there are any questions, just drop a comment below.
