---
title: "Create a custom view for SCOM alerts in SCSM"
date: "2013-06-07"
excerpt_separator: "<!--More-->"
categories: 
  - "operations-manager"
tags: 
  - "microsoft"
  - "operations-manager"
  - "system-center"
---

In my last post I wrote about how to connect Operations Manager to Service Manager. The default settings after this has been done and following my guide to ship alerts from SCOM to SCSM is that every incident is just sorted under “All Open Operations Manager Incidents”. This view is fine when you’r just managing a small environment with a couple of servers, not so much fun when managing a couple of hundred servers since it gets really messy. One of the first thing that i did after connecting the products was that i created my own custom views in Service Manager, one view per management pack or function. I will demonstrate how you can make a custom view that contains only the alerts generated for Citrix XenServer, VMware ESXi and of course, Hyper-V 3.0.
<!--More-->
### How to create the view

Open up your Service Manager console and browse to Work Items and then you will see the “All Open Operations Manager Incidents” among other views.

![](https://blog.orneling.se/assets/images/2013/06/060713_1310_Createyouro1-300x239.png)

Right click “Incident Management” and choose “Create View”

Name the view Hypervisor Alerts for example

Under “Criteria”, click browse and search for Operations Manager-Generated Incident as in the picture below:

![](https://blog.orneling.se/assets/images/2013/06/060713_1310_Createyouro2.png)

Then click OK and it will look like the following picture:

![](https://blog.orneling.se/assets/images/2013/06/060713_1310_Createyouro3.png)

In “Available properties” choose both Management Pack Name and Status. The status will do fine with just active for now, this way it will only show open incidents. In Management Pack Name, type the ID of the Operations Manager Management Pack (right click the MP in the SCOM console and choose Properties to find the ID). I will sort incidents for XenServer, ESXi and Hyper-V and I will do this once per every MP.

![](https://blog.orneling.se/assets/images/2013/06/060713_1310_Createyouro4.png)

Scroll down to Display and choose which parameters you would like to see. I´ve chosen Description, Display Name, Management Pack Name, Name, Priority and Source and then click OK.

Your view is now created and should look like the below picture.

![](https://blog.orneling.se/assets/images/2013/06/060713_1310_Createyouro5.png)

### Testing the view

Since the view came out empty, of course I want to test the view and connections to make sure they show up when they are generated.

After killing the Virtual Machine Management Service on the Hyper-V host (shut down the VM’s before you ever think of doing this), the following incident show up and the view is functional.

![](https://blog.orneling.se/assets/images/2013/06/060713_1310_Createyouro6.png)

### Summary

This view that I´ve just created is really simple to set up and it will make life easier for your support technicians that are working in the Service Manager console.

As always, if there are any questions just leave a comment.
