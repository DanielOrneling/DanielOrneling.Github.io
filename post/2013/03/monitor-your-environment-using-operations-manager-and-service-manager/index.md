---
title: "Monitor your environment using Operations Manager and Service Manager"
date: "2013-03-20"
categories: 
  - "operations-manager"
  - "service-manager"
tags: 
  - "microsoft"
  - "operations-manager"
  - "system-center"
---

Sometimes, System Center Operations Manager can look like a very complex and difficult system to learn. There are a lot of rules and monitors to watch out and the reason for this is because most people do their monitoring directly in the Operations Console with all alerts visible.

Instead of using this method, System Center Service Manager should be used to  handle the monitoring of the environment while Operations Manager takes care of the surveillance. After implementing SCOM along with some MP’s, a lot of alerts are generated from all of the rules and monitors and the SCOM console is really messy after just a week or two. The method which i am talking about here transfers the alerts from SCOM to the Service Manager console instead. This is done via connectors that are set up by the SCOM and SCSM admins.

To connect Operations Manager and Service Manager is a real good thing to do if you already have those two products implemented in your environment and i will tell you why. When using the connectors i mentioned above, all alerts created inside SCOM are then transferred to Service Manager and all alerts creates their own incidents.

In most companies, all personnel have their different areas of responsibility, e.g. Active Directory or Exchange. Instead of showing all alerts, from AD to network alerts to every operator, different alerts can be routed to the correct group. If you receive an alert in SCOM about an Exchange issue it will be based on a specific SCOM class, this class can then generate an alert which then generates an incident based on a specific incident template. This incident is then automatically assigned to the Exchange group. This way, we make life a lot easier for our IT admins and we can receive quicker response to our problems.

The sweetest thing is that the connectors is working in both directions, when an alert is closed, the incident is updated. When an operator assigns the incident to himself or herself the Operations Manager alert are also updated with a IR ID (Incident Request ID) and you can see which operator has taken care of the incident.

As I mentioned above, there are two different kinds of SCSM connectors, the first one is the alert connector which transfers the alerts and then updates the alerts based on the SCSM input, e.g. when an incident is closed the alert in SCOM can also be closed automatically.

The other connector is the CI connector that is responsible for populating the Service Manager CMDB with all of the discovered objects in SCOM. When this connector is active, our SQL servers and other servers will show up in the CMDB. I will show you how to connect SCOM and SCSM in another post so keep visiting the blog to stay updated.

Any questions? Leave a comment and i will get back to you.
