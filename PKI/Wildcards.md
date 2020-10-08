---
layout: default
title: Wildcards
parent: PKI
---

# Wildcard Certificates
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }


* TOC
{:toc}

---

# Wildcard Deployment 

When you generate a wildcard for .example.com, you only need to complete one certificate signing request from one server. Complete the same process you normally would to generate an SSL certificate from your certificate provider. 

## Installing the Certificate on The First Server 

* Log in to the server that generated the CSR and complete the request 
* Open IIS Manager and open the site you want to connect to 
* Double click Server Certificates
* Select Complete Certificate Request
* Browse to the file the CA provided and give a friendly name for the certificate 
* Select OK 

## Exporting the Certificate 

* Log in to the server that generated the CSR and completed the request originally 
* Open the MMC Console
* Select File -&gt; Add/Remove Snap-In 
* Double click Certificates 
* Select Computer Account 
* Select Next 
* Select Finish 
* Select OK 
* Open Certificates/Personal/Certificates 
* Right click the Wildcard and select All Tasks/Export 
* Select Next 
* Select Yes, export the private key 
* Check the box to Include all certificates in the certification path if possible 
* Give it a password 
  * This is not a password you share with anyone as that can be a significant security risk. Remember – longer, more complex passwords are better. 
* Select Next 
* Browse to a location to save the certificate and save it there 
* Select Next 
* Select Finish 
* Copy the generated certificate to the server you want to install it on 

## Deploying the Wildcard 

### Install the Certificate on Server 2 and Beyond \(Windows\) 

* Once you have exported the certificate and copied it to your computer, log in to the server you want to deploy the new certificate to and copy the certificate to it 
* Open IIS Manager and open the site you want to connect to
* Double click Server Certificates 
* Browse to the certificate and enter the password you gave it before 
* For most cases, do not let the certificate be exported 
* Select OK 

### Bind the Certificate 

* Once you have imported the certificate in IIS, keep the IIS Manager window open, and navigate to Server\*/Sites/Default Site 
* On the right side menu, select Bindings… 
* If https is not there, select Add. If https is there, select Edit 
* For IP Address, select All Unassigned 
* For Port, enter the port that will be used for the application 
* For SSL certificate, select the Wildcard friendly name you just imported and 
* Select OK.

