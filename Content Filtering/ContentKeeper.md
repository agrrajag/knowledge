---
layout: default
title: ContentKeeper
parent: Content Filtering
---

# ContentKeeper
{: .no_toc }

HTTP and HTTPS web filter
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

* TOC
{:toc}

---
# Categories

> NOTE: Many of the guides suggest syncing to slaves. If you are in a single-appliance situation, you do not need to perform this action.

## Viewing a Site’s Category

* Log in to the ContentKeeper appliance
* Select Sites
* Type in or paste the URL of the site or page
* Select Process Above Sites
* A table of pages will pop up
* You can view the current classification under the column labelled Current Classification
* If the source says LOCAL, this means someone locally has classified it this way.

> NOTE: If you used a /page in the URL, both the domain and the individual page will be available in these results.

## Changing a Site’s Category

* Follow the steps above to [view the classification](./#viewing-a-sites-category)
* Under “Your New Suggested Classification” select the classification you would like to modify it to
* Select Reclassify Above Sites
* At the top of the page, select the icon in the shape of a folder with a person inside. This is the Policy tab
* At the bottom of the page, select Sync to Slaves
* A pop-up will open and go through a list of processes
* When It is complete, a button will appear at the bottom and say Close Window

## Viewing Domains/Sites in a Local Category

* Log in to ContentKeeper
* Select the Policy button
* On the left sidebar, select Local Categories
* Find the local category you would like to search
* Select the number to the right of the category \(under URL Count\)
* A new window will pop up with all URL’s in that local category and who assigned each

# HTTPS Decryption

## Deploy the Certificate

The certificate is needed to allow HTTPS decryption of search engines and certain defined sites to work properly. The certificate does nothing for authentication, it only provides a method for decryption.

* Navigate to [https://contentkeeper.example.com/ckroot/](https://contentkeeper.example.com/ckroot/)
* Download the Root Certificate either on the computer needing it or on a flash drive
* Install the certificate based on the instructions on that page.

## Adding Search Engines and Sites to be Decrypted

* Log in to ContentKeeper
* Select the Gear for setup
* On the left side, select HTTPS/SSL Configuration
* Select Decryption Settings at the top of the page
* At the bottom in the left column, add the domain you would like to decrypt with periods and wildcards surrounding - example: `*.duckduckgo.com.*`
* Select Save and Redisplay
* Wait a while for it to update
* Select Sync To Slaves
* A pop-up will open and go through a list of processes
* When It is complete, a button will appear at the bottom and say Close Window

## Enable HTTPS Decryption for the subnet

Generally ContentKeeper has you list out all of your subnets to be bypassed in this list before enabling decryption during the initial appliance installation. This allows you to slowly roll in decryption.

* Log in to ContentKeeper
* Select the Gear for setup
* On the left side, select HTTPS/SSL Configuration
* Select Decryption Settings at the top of the page
* You will notice a list of subnets that are currently bypassed
* Locate the subnet you would like to start decrypting
* Remove the data from the row you would like to remove
* Select Save and Redisplay
* Wait a while for it to update
* Select Sync To Slaves
* A pop-up will open and go through a list of processes
* When It is complete, a button will appear at the bottom and say Close Window

> NOTE: It is OK to have a blank row in the list, it will reorganize after you save.

## Disable HTTPS Decryption for the subnet

* Log in to ContentKeeper
* Select the Gear for setup
* On the left side, select HTTPS/SSL Configuration
* Select Decryption Settings at the top of the page
* You will notice a list of subnets that are currently bypassed
* At the bottom of the list, after the OR column, type in the network ID
* A Network ID is like an IP address, but the last octet is a 0 – Like 192.168.0.0
* Enter the appropriate IP Mask in the next column – Like 255.255.255.0
* Give it a description
* Change Mode to Bypass
* Select Save and Redisplay
* Wait a while for it to update
* Select Sync To Slaves
* A pop-up will open and go through a list of processes
* When It is complete, a button will appear at the bottom and say Close Window

# Reports

## Live Reports

* Log in to ContentKeeper
* Select Reporting
* On the left sidebar, select Live Viewer
* Data will be coming in quick, select Pause
* Open Advance filters and add whatever filters you would like \(common is Device IP\)
* Select Done when you have the filters you want
* Select Resume to start watching live filtered data.

## Historical Reports

### Generate Reports

* Log in to ContentKeeper
* Select **Reporting**
* Select **Advance Filters**
* Add the filters you want \(Typically Device IP, Allow/Block, and Event Time\)
* Select **Done**
* Wait for the report to generate.

### Exporting Reports

* Follow the process to generate the report
* Select the **Schedule** button on the right \(Even if you only need this completed one-time\)
* Give it a title - generally the work order number and requestor
* Select the **OUTPUT** you would like to download
* You do not need to enter an email address
* Select Submit
* On the left, go to **Report History**
* Select the hamburger button next to the desired report under Actions
* Select either **View** or **Download**
* Select **Submit**

# Exclusions

## Authentication Exclusion

If you have a device in an awkward IP range that is not properly pulling authentication, you can bypass the authentication aspect and have it pull the default ruleset.

* Log in to ContentKeeper
* Select Administration
* Select Users and Groups on the left
* Select the Username Resolution tab on the top
* Select the "Bypassed IP's" button at the bottom of the page
* Enter the IP address, mask, and description of the device
* Select Save and Redisplay
* Go to Policy
* Select Sync to Slaves
* If you have multiple devices, log in to your other devices and confirm the bypass setting is applied to it as well, if not, add it.

## Filter Exclusion

* Log in to ContentKeeper
* Select Administration
* Select Excluded IP Addresses
* Enter the IP Address, prefix length, change mode to Excluded, and enter a description
* Select Save and Redisplay
* Go to Policy
* Select Sync to Slaves
* If you have multiple devices, log in to your other devices and confirm the bypass setting is applied to it as well, if not, add it.