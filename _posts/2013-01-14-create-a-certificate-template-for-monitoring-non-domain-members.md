---
title: "Create a certificate template for monitoring Non-Domain members"
date: "2013-01-14"
excerpt_separator: "<!--More-->"
categories: 
  - "operations-manager"
tags: 
  - "microsoft"
  - "operations-manager"
  - "system-center"
---

To monitor servers that aren´t in your domain but in a DMZ, a server certificate is required. In order for this to work properly, a Certificate Template needs to be created before you can issue your certificates. The following will guide you through the process of creating the Certificate Template so that you can monitor your non-domain members in the future.
<!--More-->
#### Do i have a Certificate Authority?

Run the following line in CMD and you will see all the CA´s in the domain

- certutil -config – -ping

#### Creating the template

1. Connect to the server that has the CA role
2. Start the Certification Authority console from in the Administrative Tools menu
3. In the console go to _**Certificate Templates**_ folder, right click on it and choose Manage
4. The Certificate Templates Console will now be launched
5. In this console you can see all of the existing certificate templates in your environment.
6. In the middle pane of the Certificate Template console you need to look for the certificate template called **Computer**
7. Right click on it and select **_Duplicate Template_**
8. If your CA is installed on a Windows Server 2008 you’ll get this window:

![](https://blog.orneling.se/assets/images/2013/01/1.png)

1. Select **_Windows Server 2003 Enterprise_**. If you would select Windows Server 2008 Enterprise you could bump into the issue that you won’t be able to see the template using web-enrollment and won’t be able to use the certificate template for OS’s pre-VISTA. Stick to the default setting in the case and click OK. Note: If the CA is Windows Server 2003 or earlier you won’t get this window.
2. The Properties window for this new certificate template will open
3. Give the template a name, e.g. OpsMgr Certificate Template
4. Under **_Request handling tab_, s**elect the **_Allow private key to exported_**
5. In the **_Subject Name_** tab you need to change the setting to **_Supply in the request_**.
6. Go to the **_Security_** tab and change settings for _Authenticated Users_ by checking the boxes for **_Enroll_** and **_Autoenroll_**. This depends on your origanizations security requirements.
7. Go to the **_Extensions_** tab. If you used the Computer certificate template like indicated in the beginning of this blog it should be OK
8. Make sure that your certificate looks like the picture below with the Application Policies and click OK.

![](https://blog.orneling.se/assets/images/2013/01/2.png)

### Publish the Certificate Template

1. Open the certificate template to settings again before publishing the template
2. Before you can use the certificate in web-enrollment you need to publish it
3. Close the Certificate Templates Console and go back to the Certification Authority console
4. Right click on the Certificate Templates, click **_New_** and **_Certificate Template to Issue_**
5. A new window will open where you can select the certificate template that you have just created, click OK to confirm and that’s it.
6. You now have  a certificate Template that may be used for issuing server certificates.
