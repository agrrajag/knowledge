---
layout: default
title: Nutanix
parent: Virtualization
---

# Nutanix
{: .no_toc }

Hyperconverged Virtual Cluster
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

* TOC
{:toc}

---

# Health Checks

Health Checks help you see what is going on in the cluster and give you knowledge-base articles on how to resolve issues that it finds. There are times where health checks will return a false-positive. Nutanix Support can help you determine if these are false-positives or real issues that need resolution.

## Prism

* After you log in to PRISM, you are greeted with the Health dashboard
* If you do not see a Green Heart, something has errored that needs to be resolved
* Select the dropdown arrow next to Home
* Select Health
* Navigate to the red or yellow dots to see where something has errored
* Some errors won’t clear for 4 to 24 hours after you resolve the issue.

## Nutanix Command Line

* Log in to Prism
* Select the cluster name at the top-left of the screen
* Take note of the cluster virtual IP address
* Open Putty
* SSH into the IP address of the cluster
* Run NCC health checks

```text
ncc health_checks run_all
```


# Data Protection, Guest Tools, and Recovery

## Nutanix Guest Tools

Nutanix Guest Tools includes a Volume Shadow Service writer to help with application-consistent \(quiesed\) snapshots and self-service restoration.

**Application-Consistent Snapshots**  
These allow you to have better backups of Microsoft SQL server and Microsoft Exchange.

**Self-Service Restoration**  
This tool allows you to do [File-Level Restores](#file-level-recovery) from the desktop of the entity you are trying to restore. You do not need to initiate this from Prism.

### Deployment of Nutanix Guest Tools

#### Windows Server Core

* Ensure the VM you are about to deploy NGT to has a CD/DVD ROM connected to it and has VMTools installed.
* Log into Prism
* Select the dropdown at the top left of the webpage to change to the VM Menu
* Select Table to pull up a list of VM's
* Select the VM you would like to deploy to
* Select Manage Guest Tools
* Select Enable Nutanix Guest Tools
* Select Mount Nutanix Guest Tools
* RDP or console into the server you would like to install NGT on
* Log in as an administrative user
* Switch to the cd drive, typically D:
* Run setup.exe
* Follow the prompts on the GUI that will pop up

#### Windows Server with a GUI

* Ensure the VM you are about to deploy NGT to has a CD/DVD ROM connected to it and has VMTools installed.
* Log into Prism
* Select the dropdown at the top left of the webpage to change to the VM Menu
* Select Table to pull up a list of VM's
* Select the VM you would like to deploy to
* Select Manage Guest Tools
* Select Enable Nutanix Guest Tools
* Select Mount Nutanix Guest Tools
* Select Enable Self Service Recovery
* Connect to the VM using either RDP or the remote console
* Run the installer in the CD Drive
* Eject the Nutanix Guest Tools when complete

#### Linux

* Ensure the VM you are about to deploy NGT to has a CD/DVD ROM connected to it and has VMTools installed.
* Log into Prism
* Select the dropdown at the top left of the webpage to change to the VM Menu
* Select Table to pull up a list of VM's
* Select the VM you would like to deploy to
* Select Manage Guest Tools
* Select Enable Nutanix Guest Tools
* Select Mount Nutanix Guest Tools
* Select Enable Self Service Recovery
* Connect to the VM using either RDP or the remote console
* If the Nutanix Tools disk loads on the desktop of the linux box, open the location in Terminal 
* Navigate to the install folder

```text
cd /media/USER/NUTANIX_TOOLS/installer/linux/
```

* Run the installation script

```text
sudo /media/USER/NUTANIX_TOOLS/installer/linux/install_ngt.py
```

> **NOTE**: There may be some dependencies to install for this process to work. It will tell you in the error if you need to install any missing dependencies

## Configuring Protection Domains

### Adding a new Protection Domain

This will configure an Async DR Protection Domain - which allows snapshots on the same storage cluster. Metro Availability is when you run snapshots on a similar remote cluster with a storage container of the same name. With Async DR's you can group machines together by snapshot schedule.

* Log in to Nutanix Prism
* On the top left, select the menu dropdown and go to the Data Protection menu
* Select **+ Protection Domain** on the top left
* Select **Async DR**
* Give the Protection Domain a name \(no spaces, but you can use dashes\)
* Select an Entity you would like to protect
* Select **Create a new CG** and name the consistency group
* If you are backing up Microsoft Exchange or Microsoft SQL and need an "application consistent" or  quiesced snapshot, select **Use application consistent snapshots**
* Select **Protect Selected Entries**
* Continue to add up to 50 desired entities if needed to that Protection Domain \(All will be snapshotted at the same time\)
* When you have all the machines you want to add to that protection domain, select **Next**
* Add the schedule you would like the snapshot to complete
* Modify the retention to keep the last x amount of snapshots
  * If you do a schedule for less than 30 minutes, it will not allow you to do an application consistent snapshot and will move to keeping the last x hours instead of last x snapshots.
* If you are adding Microsoft Exchange or SQL to the snapshot, enable **Create application consistent snapshot**
* Select **Save**

> **NOTE**: For application consistent \(quiesced\) snapshots, that setting must be enabled on **BOTH** the entity and schedule for it to perform that action.

## System-Level Recovery

* Log in to Nutanix Prism
* On the top left, select the menu dropdown and go to the **Data Protection** menu
* If not already in Table view, select **Table** at the top of the page
* Select the protection domain the entity you want to restore is located in The bottom half of the page should have updated
* Select **Local Snapshots**
* Select **Restore** next to the snapshot you would like to use to restore the entity
* Select the **checkbox** next to the entity you would like to restore
* If you want it to restore-in-place, select the radio button for **Overwrite existing entities**
  * If you do not want to overwrite, create a new entity and give it a path.
* Select OK
* Wait for the process to complete
* Check vCenter for updates as well
* When complete, if the machine is not already powered up, spin up the machine.

## File-Level Recovery

### Windows with a GUI

It is likely that the Nutanix SSR Application will not work on the Desktop. Use the index file in the program folder to access SSR.

* Navigate to C:\Program Files\Nutanix\ssr and double click index.html
* Log in using your Nutanix credentials
* Select the snapshot you would like to modify
* Select the drive you would like to mount
* Select the down arrow on the right
* Select Mount

### Windows Server Core

* Remote into the server
* Navigate to c:\Program Files\Nutanix\ngtcli on the command prompt

```text
cd c:\Program Files\Nutanix\ngtcli
```

* Start Nutanix Guest Tools Command Line

```text
ngtcli.cmd
```

* Open up the snapshot recovery tool and list the current snapshots

```text
ssr ls-snaps
```

* Find the snapshot ID of the date and drive to mount \(newest on top\)
* Run this command and replace disk label and  snapshot ID with the desired snapshot to mount the drive:

```text
ssr attach-disk disk-label=scsi0:0 snapshot-id=000000
```

* Once it says attached successfully, open a finder window on your local computer and navigate to [\\machinename\F$](file://machinename/F$)
* Copy the files from the F drive to their original location
* When you are done fixing the file issues – run this command to dismount the snapshot

```text
ssr detach-disk attached-disk-label=scsi0:0
```

# Storage

## Disk Usage and Deduplication

* Log in to PRISM
* Select the dropdown arrow next to Home
* Select Storage
* Select the Table tab
* Select the container
* You can view usage details and deduplication efficiency from this screen.

# Upgrade Sequence (AOS 5.15)

[Nutanix Acropolis 5.15 Official Upgrade Guide](https://portal.nutanix.com/page/documents/details/?targetId=Acropolis-Upgrade-Guide-v5_15%3AAcropolis-Upgrade-Guide-v5_15)

Log in to Prism and perform this upgrade sequence:

> If you have Prism Central (PC) , upgrade PC first then run NCC

## Download and update NCC
* Log into Prism
* Select the gear at the top right
* Select Upgrade Software on the left
* Select the NCC tab
  * If there is a new version, select Download next to the new version, then select Upgrade when it has downloaded

## Run NCC checks
* Select the down arrow next to Settings at the top left of the screen
* Select Health
* Select Actions at the top right of the screen
* Select Run NCC Checks
* Make sure "All Checks" is selected
* Select Run
* Wait for the email that will be sent to see if there are any major issues with the cluster
>  Contact Nutanix Support if any major issues occur during the NCC Checks that you don't know how to resolve

## Upgrade Foundation
* Select the gear at the top right
* Select Upgrade Software on the left
* Select the Foundation tab
  * If there is a new version, select Download next to the new version, then select Upgrade when it has downloaded

## Run Lifecycle Management (LCM) Inventory (do not upgrade software yet)
* Select the down arrow next to Settings at the top left of the screen
* Select LCM
* Select the Inventory tab on the left of the screen
* Select Perform Inventory at the top of the screen
* Select Run
> Don't worry about performing auto inventories. This will cause the cluster to have a REST API error every night it auto-inventories.

## Upgrade AOS

* After running LCM, go to Updates/Software
* Select the AOS checkbox and make sure it is to the version you would like to move to
* Select Install
* Wait for LCM to complete the process
  * This will take a long time to complete

## Upgrade Firmware

Make sure to complete firmware upgrades BEFORE upgrading AHV. It is common that you will see errors for an incompatible AHV version during this process.

* Run LCM Again
* After running LCM, go to Updates/Software
* Select all devices
* Select Update
* Select Next
* Enter in vCenter administrator information
* Select Next to begin the install
  * This will take an extended period of time. It will update firmware, BIOS, and other critical resources on each physical host. You can monitor the install progress by connecting to the IPMI of each device.

## Upgrade AHV

* In LCM, go to Updates/Software
* Select AHV
* Select Update
* Select Apply Updates

## Upgrade vCenter
This must be completed before you upgrade the ESXi Hypervisors in case there are any version issues!
* Log into the vCenter Web Management GUI
* Select Update on the left
* Select Check Updates on the top right
* Select Check Repository
* If an update is available, select Install Updates
* This may require a reboot of vCenter
  *	Since this is not in a High Availability cluster, this should generally be safe to do during hours. Always approach this cautiously.


## Upgrade other Hypervisors

[Nutanix and ESXi Upgrade Information](https://portal.nutanix.com/page/documents/details?targetId=Acropolis-Upgrade-Guide-v5_15:upg-cluster-hypervisor-upgrade-esx-pe-t.html) 

### Prerequisites

* Ensure LCM has upgraded firmware on the machine
* Ensure the cluster is in good health

### Grab Nutanix Metadata

* Navigate to [Nutanix Hypervisor Details](https://portal.nutanix.com/page/downloads?product=hypervisordetails) and sign in with your Nutanix account.
* Select the hypervisor, OEM, and the correct version you are looking for
* Look at the current build number and download the metadata for what you need to move to
* You will need this file when you complete the upgrade portion.

### Grab the Hypervisor Binary

* Navigate to [my.vmware.com](https://my.vmware.com) and login
* Select Product Downloads
* Select View Download Components next to VMWare vSphere (not VMWare vSphere ESXi)
* Change the version to the correct version
* Select the Custom ISO’s tab
* Expand OEM Customized Installer CDs
* Download the latest OEM Offline Bundle Zip


### Upgrade

* Log into Prism
* Select the gear at the top right of the screen
* Select Upgrade Software on the left
* Select the Hypervisor tab
* Select Upload a Hypervisor binary
* Upload the Nutanix Metadata file you downloaded
* Upload the hypervisor zip file to the Binary section
* Select Upload Now
* Run the upgrade

### Run NCC

Run NCC a few times after the upgrade. Some warnings and errors will trigger after the devices reboot (NTP errors, Stargate errors, Controller VM Reboot errors). These are ok to monitor. Give it a couple of hours before you report these to your OEM. Check and see if anything is pressing. After about 6 hours, it should stabilize and give you an accurate representation. 
