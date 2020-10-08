---
layout: default
title: Informacast
parent: VoIP
---

# Informacast
{: .no_toc }

Cisco VoIP based Public Address System
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

* TOC
{:toc}

---

> NOTE: Sessions time out quickly. Constantly save your work in order to retain changes.

# Bell Schedules \(Scheduled Messages\)

## Changing Times of Day Bell Rings \(Ring Lists\)

* Hover over Bells
* Select Edit Ring Lists
* Select Edit Next to the list you want to modify
* To add another bell, select Add Entry. 
* Enter the time you want in military time to make it easier \(14:00 for 2:00 PM\)
* Select the tone you want to use
* Select the Recipient group you want the message broadcasted to
* Click and drag the blue arrows down to the next row to copy parameters to that row
* Do not worry about the times being out of order. It will move into chronological order after the next update
* To delete a bell, select DELETE next to the bell you want to remove. 
* When you are satisfied with your changes, select DONE to update the ring list

## Changing Days of Week and Bell Schedules

* Hover over Bells
* Select Edit Bell Schedules
* Select EDIT next to the bell schedule you would like to edit and choose one of the tasks below:

> **To change a bell schedule for only one specific day or range, select ADD ENTRY next to Exceptions**
>
> * Select Add Entry
> * Set a description for it
> * Set the start day of that event
> * Set end date for that event
> * Change Ring List to whichever one you want
> * Select Add
> * Select Done on the next screen
>
> **To change a bell schedule for a specific day every week**
>
> * Find the day you want to change in the bell schedule
> * Choose the ring list you would like to use on that day
> * Select Done
>
> **It’s the beginning of the school year and my bells aren’t ringing**
>
> * Navigate to your bell schedule
> * Near the top, set the start date for the school year
> * Set the end date for the school year
> * Select Done

# Messages

## Stopping Informacast Messages

* Hover over Messages
* Select Send or Edit Messages
* Near the top, select View to view actively playing broadcasts
* Select STOP next to the message you would like to stop

## Starting Informacast Messages

* Hover over Messages
* Select Send or Edit Messages
* Select SEND next to the message you would like to send
* Select the recipient group you would like to send the message to or type in the extension at the bottom of the screen
* Select SEND

# Machine to Machine \(M2M\)

## Disable/Enable an M2M Contact Closure

* Sign in to Informacast
* Hover over Plugins
* Select M2M
* Select Contact Closures
* Click the “\#” Input Port of the relay you are trying to modify
* Select the name of the trigger
* Next to Monitoring Status, select Disabled or Enabled depending on desired task
* Select Save

# Informacast and CUCM

## Setting Up CUCM and Phone Services

### Find the Service URL

* Sign in to Informacast
* Hover over Messages
* Select QuickPage Assistant
* Select the desired message next to “Send Message”
* Select the desired recipient group next to “To Groups”
* Enter the Informacast username you would like to use to make the message \(this will show in message reports\). Do not use your personal Informacast username.
* Enter that user’s password
* At the bottom, you will see a URL you can copy. Example:
* `http://x.x.x.x:xx/InformaCast/phone?message_key=000&recipient_group_key=0000&login=test&password=test&DN=auto`

