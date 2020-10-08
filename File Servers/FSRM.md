---
layout: default
title: Microsoft FSRM
parent: File Servers
---


# Microsoft File Server Resource Manager \(FSRM\)
{: .no_toc }

Disk Quotas and File Server Management
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

* TOC
{:toc}

---

## Quota Management

This allows you to set quotas \(folder size limits\) on folders located on your file server. This is a good tool if you want to apply a blanket quota for many folders inside of a parent folder \(such as the location where you store user's home folders\)

### Checking Quota Limits for a Folder

* Open File Server Resource Manager \(FSRM\)
* Right Click File Server Resource Manager \(local\)
* Select Connect to Another Computer
* Select the radio button for Another Computer
* Type in the name of your file server
* Open Quota Management / Quotas
* Wait a short period for it to generate the list
* Locate the folder you would like to check
* On the same row, you will see quota limits, % used, quota type, and if it is matching the template assigned

### Modifying Quota Limits for a Specific Folder

* Open File Server Resource Manager \(FSRM\)
* Right Click File Server Resource Manager \(local\)
* Select Connect to Another Computer
* Select the radio button for Another Computer
* Type in the name of your file server
* Open Quota Management / Quotas
* Wait a short period for it to generate the list
* Right click the folder you would like to modify
* Select Edit Quota Properties
* Change the limit to new desired limit
* Select OK

> NOTE: Be cautious of available space on the server you are modifying.

## File Screening

### Modifying File Screens

* Open File Server Resource Manager \(FSRM\)
* Right Click File Server Resource Manager \(local\)
* Select Connect to Another Computer
* Select the radio button for Another Computer
* Type in the name of your file server
* Open File Screening Management / File Screens
* Open the file screen you would like to modify

