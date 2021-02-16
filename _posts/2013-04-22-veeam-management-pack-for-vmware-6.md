---
title: "Veeam Management Pack for VMware 6"
date: "2013-04-22"
excerpt_separator: "<!--More-->"
categories: 
  - "operations-manager"
tags: 
  - "microsoft"
  - "operations-manager"
  - "system-center"
---

Earlier this year, I wrote a blog post about how to monitor your VMware environment. The solution that Veeam has come up with consists of three components; the Enterprise Manager, an Enterprise Manager User Interface and a collector. The solution, which I wrote about here were based on version 5.7 of the Veeam MP.

A couple of weeks ago, Veeam launched their latest updated release of the MP version 6.0. In this release, the solution has been almost completely rebuilt and there are really a lot of news. Below, i will go through some of the news in this release and why you should implement this in your environment.
<!--More-->
### Storage features

**• Storage topology:** Maps virtual machines (VMs) to the storage where they run. You can dive into real-time dashboards and monitor key metrics on latency, provisioning and utilization.

**• Network topology:** Maps VMs to the software-defined network components. Allows you to view per-switch usage and packet analysis. Veeam MP v6.0 fully supports Distributed Virtual Switches, including the Cisco Nexus 1000V.

**• Compute topology:** Allows you to view hosts, their physical hardware, the logical hypervisor components and the VMs they are running.

### Dashboard features

Veeam MP v6.0 has over 30 new dashboard views that leverage the new System Center 2012 Operations Manager dashboard widgets, giving you real-time performance views for your critical vSphere systems. You can view on-demand, in-context dashboards, such as the ‘Top 10 hosts for CPU’ per-cluster and ‘Top 10 VMs for Disk I/O’ per datastore.

### New platform support

• VMware vSphere 5.1

• Microsoft Windows Server 2012

• Microsoft System Center 2012 SP1

Look into more of the news at Veeams website [here](http://www.veeam.com/vmware-microsoft-esx-monitoring.html?ad=menu){:target="_blank"}.

Right now, Veeam runs a campaign where you, if your a new customer can receive a free licence. This license covers up to 10 CPUs and spans over a year (after that first year, you’ll have to pay for support). If your running 5 dual CPU hosts, this licence will cover your needs. Read more about this offer [here](http://www.veeam.com/freemp?ad=mp-next-steps){:target="_blank"}.

If you have any questions, leave a comment and i will answer as soon as possible. I have tried this new MP both internally and at customer sites so just leave a footprint if you’r wondering about anything.
