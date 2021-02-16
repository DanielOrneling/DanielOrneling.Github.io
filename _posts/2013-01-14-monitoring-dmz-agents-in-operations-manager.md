---
title: "Monitoring DMZ Agents in Operations Manager"
date: "2013-01-14"
excerpt_separator: "<!--More-->"
categories: 
  - "operations-manager"
  - "orneling-se"
---

Quite often, i run into customers that are using a DMZ for hosting their web servers and sites. Since they don´t share the domain with the other servers, such as DC´s and Sharepoint servers monitoring can be a little tricky the first time. This is possible using either gateway servers or just server certificates. The difference is that when the DMZ servers are in a separate domain, a Gateway server can be used instead of just a certificate.
<!--More-->
This guide will focus on using server certificate for a DMZ server that acts as a stand-alone-server in the DMZ.. This requires that a Certificate Template is created in your environent, read more about how to do this [**_here_**](http://blog.orneling.se/2013/01/create-a-certificate-template-for-monitoring-non-domain-members/){:target="_blank"}

Please note that the following procedure **must** be performed on both the Management Server and the DMZ servers for proper function. The guide requires all of the steps where you create the certificate to be performed on the Management Server.

To obtain a server certificate, follow these instructions:

### Create a certificate request

1. Create a folder, e.g. C:\\DMZ
2. In this folder, create a new text file with the following text;
3. _\[NewRequest\]_
4. _Subject=”CN=SERVER-FQDN”_
5. _Exportable=TRUE_
6. _KeyLength=2048_
7. _KeySpec=1_
8. _KeyUsage=0xf0_
9. _MachineKeySet=TRUE_
10. _\[EnhancedKeyUsageExtension\]_
11. _OID=1.3.6.1.5.5.7.3.1_
12. _OID=1.3.6.1.5.5.7.3.2_
13. Save the file with the name SERVERNAME.inf in the folder you just created
14. Run CMD as an Administrator
15. Change Path to C:\\DMZ
16. Run the command line “CertReq -New -f RequestConfig.inf SERVERNAME.req”
17. In the folder, a file shows up with the name SERVERNAME.req
18. Open this file in Notepad and copy all of the content in the file

### Obtain the certicate

1. Navigate to http://CERTSRV/certsrv/ in Internet Explorer
2. Click “Request a certificate”
3. Click “advanced certificate request”
4. Click “Submit a certificate request by using a base-64-encoded CMC or PKCS #10 file, or submit a renewal request by using a base-64-encoded PKCS #7 file.”
5. Paste the content you copied from the INF file in the step .8, in Certificate Template choose “Operations Manager” and then click Submit
6. Choose Base 64 encoded and click Download certificate, save the file to the folder C:\\DMZ

### Obtaining the CA Root Certificate

1. Navigate to http://CERTSRV/certsrv/ in Internet Explorer
2. Click “Download a CA certificate, certificate chain, or CRL”
3. Choose Base 64 and click “Download CA certificate chain”, save the file to C:\\DMZ

### Import and Export the certificate

Only perform steps 1 – 6 for the Management Server

1. Click Start, type MMC in the Search bar and then click File, Add/Remove Snap-in
2. Add Certificate and then choose Computer account, click Next and then Finish
3. Expand Certificates until you see Personal -> Certificates. Right click Certificates and choose All Tasks / Import…
4. Click Next and then Browse…
5. Browse to the C:\\DMZ folder and choose the appropriate server certificate and click Open
6. Click Next twice, then click Finish
7. The next step is to Export the certificate with the private key so you can import it on the appropriate server.
8. Right click the certificate that shows up in the right window and choose All Tasks / Export…
9. Choose “Yes, export the private key” and click Next twice
10. Type in a password, e.g. SCOMCERT and click Next
11. Click Browse and browse to C:\\DMZ and type in the server name and then click Save

### Import the certificate on the server that´s about to be monitored

Skip this steps for the Management server.

1. Log on to the server for which you just exported a server certificate, e.g. DMZMACHINE.lab.local
2. Copy the exported server certificate and the root certificate (certnew.p7b) to a folder on the server
3. Click Start, type MMC in the Search bar and then click File, Add/Remove Snap-in
4. Add Certificate and then choose Computer account, click Next and then Finish
5. Expand Certificates until you see Personal -> Certificates. Right click Certificates and choose All Tasks / Import…
6. Click Next and then Browse…
7. Browse to the folder where you putted the certificates and choose the server certificate and click Open and then Next
8. Type-in the Password that you set in step .28 and then click Next twice
9. Click Finish and the certificate is then imported
10. Next step is to import the Root CA Certificate
11. In the same window as the certificate you just imported, expand Trusted Root Certification Authorities and click Certificates
12. Check if your enterprise root CA shows up in the right window, if it does no action is needed since the certificate is already imported
13. If the enterprise root CA does not show up, right click Certificates and choose All Tasks / Import…
14. Click Next and then Browse, browse to the folder where you copied the certificates and then choose to look for “PKCS #7 Certificates (\*.spc,\*.p7b)”
15. Choose certnew and click Open
16. Click Next twice and then Finish

### Import the certificate for use with Operations Manager

1. The last step is to import the certificate to Operations Manager, this steps requires that the Operations Manager agent has been installed on the server prior to this step
2. Browse to the folder below that matches the server’s processor architecture and then copy MOMCERTIMPORT.exe to a folder on the Agent server. MOMCERTIMPORT is located in SupportTools\\AMD64 or SupportTools\\I386 on the SCOM media.
3. Run CMD as an administrator and browse to the folder where you copied the MOMCERTIMPORT file
4. Run the following command line; MOMCERTIMPORT.exe /SubjectName:SERVERNAME, e.g. MOMCERTIMPORT.exe /SubjectName:DMZMACHINE.lab.local
5. The certificate is now imported. Filter the Operations Manager event log for event ID 20053. When it shows up, the certificate has loaded successfully

### Allowing the agent to communicate with the Management Server

The final step to allow the new agent to communicate with the management server is to Approve the agent.

1. In Operations Console -> Click the Administration Tab -> Click pending management
2. Mark the servers that show up in the right window and click Approve. The agent will now start communicating with the management server.
