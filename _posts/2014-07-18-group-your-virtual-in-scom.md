---
title: "Group your virtual machines in SCOM"
date: "2014-07-18"
excerpt_separator: "<!--More-->"
categories: 
  - "management-packs"
  - "operations-manager"
tags: 
  - "scom"
---

For a while, I´ve been struggling with a problem when configuring Operations Manager. As a consultant, I run into a lot of different issues to solve and one day isn’t like the other. However, this doesn’t mean I never run into the same issue twice. My problem have been to group all virtual machines in Operations Manager several times now. This is easy, at least if your VM´s are running on Hyper-V. So, what if you’re running your virtual machines on VMware? After having imported the management pack for Windows Server, there is a property named “Virtual Machine” that you can include in the views that comes with the MP or your custom views. This property however is only populated by Hyper-V machines leaving the VMware VM´s outside. My solution to this problem has been to write a new Management Pack that (so far) does the below things:
<!--More-->
- Discover VMware Tools that are running on the servers by scanning the registry for the ImagePath property which lies in the VMTools folder. The path for the property is HKEY\_LOCAL\_MACHINESYSTEMCurrentControlSetServicesVMToolsImagePath
- When the registry key is found, the property that I mentioned above (Virtual Machine) will be populated by those VM´s where VMware Tools is installed. This will then show up as “Virtual Machine: True” in the views.
- Once VMware Tools has been found, the service will also be monitored by Operations Manager. If the VMTools service stops, an alert will be generated about the outage.
- A group is created which contains all the virtual machines in the environment. The group is built with a dynamic membership query which basically includes the servers (Windows Computer) where Virtual Machine equals True.
- A folder has been created in the Monitoring pane which contains a view showing virtual machines and the VMware Tools status of the servers.

### Why do I need this management pack?

Well, I need this MP to sort out my VM´s so I can make overrides aiming at virtual machines only. This is also a better solution than creating custom attributes and then trying to create a dynamic group based on those attributes. That´s something that seems to be impossible in SCOM 2012, hence this management pack. (Ok, I admit Management Authoring is a lot funnier than building attributes as well :)

### How to install the Management Pack

Installing the MP is really a piece of cake, just download it from my OneDrive here and import it into Operations Manager. This first version is unsealed so feel free to edit the MP if you feel like it.

### How does it look?

Look below for a quick view of the MP. The picture shows the view I´ve created and this is how it will look upon the import of the MP.

![](https://blog.orneling.se/assets/images/2014/07/2014-07-18_14-19-23-1024x493.jpg)

### Wrap up

I will keep developing this MP and my plan is to be able to include servers running on XenServer as well but that’s for later. Comments on the MP are more than welcome and i hope I will be able to help some of you with grouping the virtual machines in your environment by writing this management pack.
