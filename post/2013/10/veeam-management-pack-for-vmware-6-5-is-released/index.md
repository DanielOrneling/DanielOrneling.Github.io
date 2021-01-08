---
title: "Veeam Management Pack for VMware 6.5 is released"
date: "2013-10-17"
categories: 
  - "operations-manager"
---

For those of you that have been around since i started this blog about 10 months ago, you will know that I´ve previously written about Veeams Management Pack for VMware twice. The [first](http://orneling.se/monitor-your-vmware-environment-using-veeam-mp/ "first") post handled the 5.7 version of the MP and the [second](http://orneling.se/veeam-management-pack-for-vmware-6-0/ "second") post handled the 6.0 version. Now it´s time for the third update, the 6.5 version that were released yesterday. In this post i´ll just go through the news in this version and in the next post i will go through the installation and configuration process.

So, what´s new in Veeam Management Pack for VMware 6.5?

### Enhanced fault tolerance

If vCenter goes down, the Veeam MP will automatically reconfigure so that data is collected directly from the hosts instead. This makes sure that there is no outage in the data collection. When vCenter comes back up, Veeam MP will return to its original state.

### Configuration tracking

If you´r having problems in the environment, Veeam MP can now show when and if changes have been made to the environment so that you can relate the problems to the changes made.

### Veeam Backup & Replication monitoring (New)

If you´r also running Veeam Backup & Replication, then Veeam MP can now also monitor those components. Veeam MP will provide monitoring, status, availability, performance and reporting for your backup solution.

### Supported configurations

Support has been added for System Center 2012 R2 Operations Manager and Windows Server 2012 R2 which will both be released tomorrow.

Other than the above, support has also been added for ESXi 5.5 and vCenter 5.5

Read more about the news at [Veeams website](http://veeampdf.s3.amazonaws.com/new/veeam_mp_6_5_whatsnew_en.pdf?AWSAccessKeyId=AKIAJI4MX44AEVG3NBLA&Expires=1381999936&Signature=rKPqqMNfEGuLoxWnZXC67RLzqcI%3D).

 

As i mentioned in the beginning of the post, only the news will be covered in this post and i will publish another post in the nearest future where I´m going through the installation process. Any questions? Just leave a comment.
