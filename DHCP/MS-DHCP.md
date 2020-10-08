---
layout: default
title: Microsoft DHCP
parent: DHCP
---


# Microsoft Dynamic Host Configuration Protocol \(DHCP\)
{: .no_toc }

Assigning IP addresses
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

* TOC
{:toc}

---

## Setting the DHCP Reserved Address \(If not already assigned\)

* Open the DHCP Management Tool
* Right Click DHCP
* Select Manage Authorized Servers
* Select your DHCP server
* Select OK
* Expand your server name
* Expand IPv4
* Expand the scope you would like to modify
* Select Address Leases
* Locate the IP address the current lease is found
* Right click the device
* Select Add to Reservation
* Go back to the tree and select Reservations
* Double click the reservation you want to change

  > * There is a glitch in DHCP where the properties of the reservation have to first be opened before it will allow you to modify properties

* Go back to the reservations folder
* Right click the same reservation
* Select Properties
* Copy the MAC address
* Select Cancel
* Right click reservation
* Delete current reservation
* Right click in white space
* Select new reservation 
* Give it the desired IP address

  > * Do a ping of that IP first to make sure there are no statically assigned devices or ip address conflicts

* Give it a name
* Paste the MAC address
* Leave Supported Types as both
* Select Add
* Restart the device
