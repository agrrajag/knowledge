---
layout: default
title: Carbon Black
parent: NGAV
---

# Carbon Black
{: .no_toc }

Next-Gen Antivirus and Endpoint Detection and Response
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

* TOC
{:toc}

---
# Endpoints

Endpoints are the computers that are connected to Carbon Black.

## Installing Sensors

### Download Sensor Kit

* Log into the Carbon Black management website
* Select Endpoints
* Select Sensor Options at the top right of the screen
* Select Download Sensor Kits
* Select Download Kit next to the sensor you would like to deploy

### Obtain Company Code

* Log into the Carbon Black management website
* Select Endpoints
* Select Sensor Options at the top right of the screen
* Select Company Codes
* Copy the registration code in the gray box.

### Deploy Sensor

* Copy the sensor deployment files to the new computer
* Open a terminal and run one of the following commands

> NOTE: You will need to update the installer version and company code before running the script. 

#### Windows
If you want the CLI users to be a group other than the default local administrators group, you will need to modify the SID for that group.

```
msiexec /q /i "installer_vista_win7_win8-64-0.0.0.0000.msi" /L* log.txt COMPANY_CODE=ABCDEF01#ABCDEF CLI_USERS=S-1-2-34-567
```

## Updating Sensors
* Log into the Carbon Black management website
* Go to Endpoints
* Select All Sensors on the top left
* Select the checkbox next to the device name you would like to update
* Select Take Action
* Select Update Sensors
* Select update sensors on the # of selected devices
* Select the latest version
* Check the box that you understand that devices may be rebooted
* Select Update

> NOTE: Once you click Update Sensors, it does not do so immediately. It will span approx. 4 hours to install.

## Grouping Sensors

### Required Knowledge

When viewing the groups, filtering of those groups is applied in a top-down approach. If my machine is both included in the filters for the top group as well as the bottom group, I will ONLY get added to the top group. If I move the top group to the bottom of the list, I will then bounce to other group since it will be over that original top group.

Also, when you modify a group in any way, it will wait two minutes before processing your changes, giving you time to modify any other group. Once that countdown timer has ended, it will take a few minutes for it to process and for the changes to be reflected.

### Adding Groups

* Log into the Carbon Black management website
* Go to Endpoints
* Select Add Group at the top right of the screen
* Enter a name
* Enter the criteria you would like to use to filter the groups
* Select the policy you would like to apply to those sensors
* Select Save

### Modifying Existing Groups

* Log into the Carbon Black management website
* Go to Endpoints
* Add or remove an endpoint if desired
    * Hover over the group you would like to modify
    * Select either the + (add) or – (delete) button next to a filter.
    * Enter the rule for that filter
* Change the policy if desired
* Change the filtering group order on the left if desired by grabbing the icon next to the group name and modify the order of that group
* Select Save

# Alerts
Alerts are logs where Carbon Black has performed an action that will be good to look over, such as the blocking of programs or the detection of viruses and malware.

## Needed Knowledge:

### Reputation Response Behavior

> NOTE: This behavior knowledge is needed for understanding alerts and investigations in Carbon Black.

Items begin at 11 and work their way down to a 1. The goal would be to get items around an 8 or 9. This would mean they are still tested for known malware, PUP’s, but typically allowed through. Items in a 2-3 are either allowed or blocked outright without testing for malware or heuristics.

[https://community.carbonblack.com/t5/Knowledge-Base/CB-Defense-Reputation-Priority/ta-p/51797](https://community.carbonblack.com/t5/Knowledge-Base/CB-Defense-Reputation-Priority/ta-p/51797)


## How to respond to an alert:

* Log into the Carbon Black management website
* Select Alerts
* Any new, non-dismissed alerts will show up in this table.
* Locate a recent alert you would like to dive into
* Select the Alert Triage button
* The event is detailed from bottom of the page up in chronological order
    * Use this to view what happened, what was invoked, and what was stopped

### If you trust the program:

* Is there a green wording on the right side that says Signed?
    * Select the Add button next to the company that program is signed by. This trusts the Certificate Authority that signed the piece of code, and will help not stop future software signed by the same code signer.
* Is there a red wording that says Not Signed?
    * This means you will have to approve the SHA-256 Hash. When you approve a hash, you are only approving that specific file being run. If there are any newer versions that come out or any changes to the hash, you will have to re-approve. A hash is only the same when it is the same exact file being executed.

### If you don’t trust the program:

* Click and drag the triage map around to see all the programs involved
* Test problem hashes or programs on VirusTotal if desired
    * Select the application
    * Select Take Action
    * Select Find in VirusTotal
    * You can view more details about this by bouncing through the tabs
* Delete the application
    * Select the hash or program
    * Select Take Action
    * Select Delete Application
    * Delete from either this device only or all devices
    * Select Delete

* Once you have taken appropriate action, select Dismiss at the top right of the screen
* Give it an appropriate reason and details
* Dismiss the alert

# Enforce

Enforce encompasses all the fine-tuning you have done to Carbon Black to make it respond the way you want it to.

## Policies

### Finding the Policies

* Log into the Carbon Black management website
* Select Enforce
* Select Policies
* Select the policy you would like to modify
    * Note: The following can’t be modified: Monitored, Standard, and Advanced
    * If you want to duplicate one of the original policies, you can select it and select Duplicate Policy

### Testing a Policy Rule

* Log into the Carbon Black management website
* Select Enforce
* Select Policies
* Select the policy you would like to test a rule from
* Select the Prevention tab
* Locate the rule you would like to test
* Select Test Rule
* Look under Your Organization to see if any events happened on any devices within the last 30 days.

### Copying Rules from One Policy to Another

Once you have a policy to work on, typically by duplicating the Standard Policy, you can start working on moving advanced policies to it.

* Log into the Carbon Black management website
* Select Enforce
* Select Policies
* Select the policy you would like to test a rule from
* Select the Prevention tab
* Locate the rule you would like to copy
* Select the Copy   button next to the name
* Select the text box
* Select or type the name of the policy you want to copy to
* Select Copy

## Reputation

Reputation contains a list of all approved and banned hashes and certificates that you have addressed in the Alerts section.

## Malware Removal

Malware Removal contains a list of all applications you have told to delete in the alerts section.