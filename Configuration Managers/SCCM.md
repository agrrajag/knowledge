---
layout: default
title: Microsoft SCCM
parent: Configuration Managers
---


# Microsoft System Center Configuration Manager \(SCCM\)
{: .no_toc }

Centralized Configuration Compliance
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

* TOC
{:toc}

---

## Boundaries
### Setting up Boundaries
* Open up the Configuration Manager Console
* Go to Administration 
* Open up Hierarchy Configuration Drop-Down
* Click on Boundaries.
* Right click in the white space and click on Create Boundary
* In the Create Boundary window enter in the information
  * Description - Can be anything
  * Type - Can be left as IP Subnet
  * Network – Insert in the subnet of the campus/building. \(10.0.1.0\)
  * Subnet Mask – The subnet mask  of the Network. \(255.255.255.0\)
  * Subnet ID- This will auto fill
  * Click OK when done.
 
### Setting Up Boundary Groups
* Open up the Configuration Manager Console
* Go to Administration 
* Open up Hierarchy Configuration Drop-Down
* Click on Boundary Groups
* By default, the Default-Site-Boundary-Group \(S01\) will be already made. 
* To create a new group right click on the white space and choose Create Boundary Group.
* In the Create Boundary window fill in the information
  * Name – Insert the name of the group
  * Description – Can be left blank
  * Under Boundaries, Select Add
    * In the Add Boundaries window, you will see a list of all the boundaries that have been created. At the moment only one has been created. 
    * Check the box 
    * Click OK
* Back to the Create Boundary Group window click on the Preferences tab
* Check the box that says “Use the boundary group for site assignment”
* On the drop down select the site if it’s not selected 
* Click Add
* Check the box by the name of the server
* Click OK 
* Click OK on the Create Boundary Group window

## Discovery Methods
### Setting up a Discovery Method
* Open up the Configuration Manager Console
* Go to Administration 
* Open up Hierarchy Configuration Drop-Down
* Select Discovery Methods
* Enable and Disable how it’s shown in the picture. Some will be enabled later on. 
* For now, we will set up Active Directory System Discovery. 
  * Right Click on Active Directory System Discovery 
  * Choose Properties
  * Click on the yellow star icon.
  * Click on Browse 
  * Choose the AD OU that will be used. 
  * Check the boxes as it shows in the picture.

