---
layout: default
title: Windows
parent: Patching

---
# Windows Patching
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

* TOC
{:toc}

---
# Windows Server Update Services (WSUS)

## Group Policy and Targeting
Group Policies can be set up to place all devices into computer groups within WSUS, define the time the computer checks WSUS for new updates, and sets up active hours in Windows 10 to ensure the machine does not install/restart during work hours. Group policies DO NOT choose which or deploy updates.

### Targeting a GPO to a WSUS Computer Group
```
Computer Configuration/Policies/Administrative Templates/Windows Components/Windows Update
```
* Enable Client-side targeting
* Type in the group name of the WSUS computer group 
    * I believe this is case sensitive.

### Setting time to check WSUS
```
Computer Configuration/Policies/Administrative Templates/Windows Components/Windows Update
```
* Configure Automatic Updates
* Scheduled install time – set the time in military time
    * Do not schedule all at the same time as you might DDOS the WSUS server.

### Modifying Active Hours
```
Computer Configuration/Policies/Administrative Templates/Windows Components/Windows Update
```
* Turn off auto-restart for updates during active hours
* Set your start and end times for when computers are active.

## WSUS Console

### Updates and Automatic Availability
Assuming all computers have been placed in their appropriate groups, these settings determine what automatically get pushed to computers.

#### Products and Classifications
```
Options -> Products and Classifications -> switch between the product and classification tabs.
```
This determines what the server will pull down from the official Microsoft Server. This does not automatically import upgrades. You can find this list in 

#### Automatic Approvals
``` 
Options -> Automatic Approvals 
```
This determines what specifically goes to each computer group. To modify which groups receive which products, you can either edit a rule or create a new one.

### Manually Importing / Deploying Updates

#### Importing updates into WSUS Console
* RDP to WSUS
* Open up the WSUS Console
* Select the server on the top left
* Select Import Updates on the top right
* The Update Catalog will open in a browser
* Search for the update you would like to push
* Find the updates and select Add to add them to your basket
* When you are done, select View Basket
* Check the box to import directly into WSUS, and select Import

#### Deploying updates
* Open the WSUS console
* Go to WSUS -> Updates -> All Updates
* Locate the update you would like to push to clients
* Right click and select Approve
* Select the 🛇 next to the computer groups you would like to deploy to.
* Select Approved for Install
* Select OK

### Cleaning Up WSUS

#### Locating Old Updates

* Open the WSUS console
* Go to WSUS -> Updates -> All Updates
* Filter the following:
    * Approval: Any Except Declined
    * Status: Any
* Right click the word Title
* Select Supersedence
* Filter by Supersedence by selecting the column
* Locate superseded updates which have either of these icons
    * Is superseded by a newer update and supersedes an older update
    * Is only superseded by a newer update

#### Declining Old/Superseded Updates
* Follow steps to locate the old updates
* Right click the superseded updates and select Approve
* Change status of All Computers to Not Approved
* On All Computers, also set it to apply to children
* Select OK
* Wait for the process to complete
* Right Click the superseded updates
* Select Decline
* Follow through any prompts and wait for the process to complete

#### Auto-Clean WSUS Disk Space
The following Powershell command will help clean WSUS

```powershell
-command Invoke-WsusServerCleanup -CleanupObsoleteComputers -CleanupObsoleteUpdates -CleanupUnneededContentFiles -CompressUpdates -DeclineExpiredUpdates -DeclineSupersededUpdates
```

# Client Registry Settings

## Force install updates from Microsoft Online
``` 
HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\
UseWUServer="0"
```

