---
layout: default
title: Video Insights
parent: Physical Security
---

# Panasonic VideoInsights
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }


* TOC
{:toc}

---

# Access
You can grant access to VI Cameras by assigning users to a security group in Active Directory.

## Adding Users/Groups to VI
Security groups are set up in Active Directory and are linked to VI on the server.

* Remote into any of the VI Servers
* In the taskbar, locate the same icon used for IP Server Manager
* Right Click the icon in the taskbar
* Select Server Configuration
* Select Network Options
* Next to “Authorized Users and Groups” select Give users or groups access to the system
* The User Tab grants admin users to VI. This should only be few key people. You will generally skip this step.
    * Select Add
    * Type the username desired
    * Press OK
* The Groups tab grants user rights to VI
    * Select the Groups tab
    * Select Add
    * Type in the name of the security group, or browse for it
    * Press OK
    * Select Apply
    * Select OK
* Restart the IP Server Manager Service
* Close out of your remote session
* Open up VI MonitorPlus on your local machine

> NOTE: You may need to restart the IP Server Manager Service on each server before it will reflect correctly in VI.

## Granting Camera Access to Groups

* Log into VI MonitorPlus as someone who has been given admin access to the cameras
* Select Administration
* Go to Users and Groups and select Setup and Configuration
* Select the Groups tab
* Select the group you want to modify
* Select the Servers the cameras needed are located on
* Locate the camera that needs permissions set
* Grant the permissions you want the group to have
* Select the Resources tab
* Select the views, maps, and rules you want that group to control
* Select OK
* Select Apply
* Select OK

# Views (Layouts)
## Creating Layouts of Cameras

* Log into VI MonitorPlus as someone who has been given admin access to the cameras
* Determine which cameras you want to set up and have the number of cameras ready
* Select Administration
* Go to Views and select Setup and Configuration
* Next to Views, select the +
* Type in the view name and select the server it will live on (place it on the server the cameras are on)
* Switch the layout type to the layout with the appropriate amount of cameras
* Click and drag the cameras from the Add Items section to the layout
* When the cameras are set up properly, select Save
* Restart VI MonitorPlus to see the changes

## Granting Layout Access to Groups

* Log into VI MonitorPlus as someone who has been given admin access to the cameras
* Select Administration
* Go to Users and Groups and select Setup and Configuration
* Select the Groups tab
* Select the group you want to modify
* Select Resources
* Check the box next under Has Permissions next to the layout you want to grant permissions to
* Select Save

# Updating Camera Servers
* Download the latest Complete DVD image from http://downloadvi.com 
* Extract the file on the desktop of the first camera server
* Run the installer as an administrator
* Select Upgrade
* Follow the prompts
* When complete, move to the next server
