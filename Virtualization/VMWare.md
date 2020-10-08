---
layout: default
title: VMWare
parent: Virtualization
---

# VMWare
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

* TOC
{:toc}

---

# Spinning Up / Down Virtual Machines

This is the equivalent of powering on/off a machine

## To Spin Up

* Log into vCenter
* You should default to the Hosts and Clusters view
* Expand the cluster if needed
* Right click the desired machine
* Hover Over Power
* Select Power On

## To Spin Down

It is highly recommended to power a machine off properly. If the machine is stuck, follow the Spin Up procedure, but select “Power Off” in the final step


# Building a new Virtual Machine

## Creation

* Log into vCenter
* You should default to the Hosts and Clusters view
* Right click the desired cluster
* Hover over New Virtual Machine
* Select New Virtual Machine
* Select Create a new virtual machine
* Select Next
* Give it a name
* Select Next to put it in the desired datacenter
* Select Next to place it in the desired cluster
* Select Next to place it in the desired storage container
* Select Next to ensure it is compatible with ESXi 6.5 and later
* Select the Operating System and Version used
* Select Next
* Determine the proper CPU, Memory, and Hard Disk resources needed
* Switch the Network to the desired VLAN
* For the CD Drive, switch to Content Library ISO File
* Select the ISO you would like to use and press OK
* Select the checkbox next to the CD drive labelled Connect
* If you need to add a second virtual hard drive, select the drop down next to New Device at the bottom
* Select New Hard Disk
* Give it the appropriate size
* Once you are happy with the build, select Next
* Confirm you are happy with the settings
* Select Finish
* Wait for the VM to build.
* Spin up the machine \(refer to earlier instructions\)
* Right click the VM 
* Select Open Console
* Install the OS
* After the OS is installed and you are logged in with a user inside console, Press CTRL + ALT
* In the menu bar, select VM
* Hover over Guest
* Select Install/Upgrade VMWare Tools
* Go back into the VM and open My Computer
* Run the installer
* Restart the server after the install has completed
* Build the rest of your server

![](/assets/vm-new.png)

# Snapshots and Recovery

## Capturing Snapshots

* Log into vCenter 
* You should default to the Hosts and Clusters view
* Expand the cluster if needed
* Right click the desired machine
* Hover over Snapshot
* Select Take Snapshot
* Name it
* Deselect “Snapshot the virtual machine’s memory unless absolutely necessary
* Select Quiesce guest file system if VMWare tools is installed
* Select OK
* Wait for progress to complete

![](assets/vm-snapshot.png)

## Reverting Snapshots

It is always best to use the snapshot manager for this operation as you can track the notes of the snapshots.

* Log into vCenter 
* You should default to the Hosts and Clusters view
* Expand the cluster if needed
* Right click the desired machine
* Hover over Snapshot
* Select Manage Snapshots
* Select the Snapshot you desire to revert to
* Select the first icon in the menu bar to revert to the snapshot
* Select Yes
* Wait for the process to complete

> NOTE: This can take a LONG time to complete

## Deleting Snapshots

Deleting snapshots tells the virtual machine to take everything from the snapshot disk and combine it to the main disk. If you have made changes, these changes would apply to the main disk. If you want to forget the changes, first revert to the snapshot, then delete it.

* Log into vCenter
* You should default to the Hosts and Clusters view
* Expand the cluster if needed
* Right click the desired machine
* Hover over Snapshot
* Select Snapshot Manager
* Select the Snapshot you desire to delete
* Select Delete
* Select Yes
* Wait for the process to complete

> NOTE: This can take a LONG time to complete

## Consolidating Disks

Disk consolidation removes the hidden files and junk left over from the Snapshot process. Every now and then, you will need to consolidate the disks. vCenter may also give the error “Disk consolidation is needed.”

* Log into vCenter
* You should default to the Hosts and Clusters view
* Expand the cluster if needed
* Right click the desired machine
* Hover over Snapshot
* Select Consolidate
* Select Yes
* Wait for the process to complete


 Extending VM Storage

> **NOTE:**
>
> * A Snapshot must not be in place if you desire to extend storage.
> * Storage extensions can occur while a Windows VM is in a spun-up state. 
> * Please ensure you have enough storage on the datastore before attempting to extend. If there is not appropriate storage, move the VM to an available datastore. 
> * The machine may need to be powered down to modify.

* Log into vCenter
* You should default to the Hosts and Clusters view
* Expand the cluster if needed
* Right click the desired machine
* Select Edit Settings
* Under the Virtual Hardware tab, locate the Hard Disk you would like to extend
* Change the number to the desired size
* Select OK.
* Wait for the process to complete

> NOTE: For a Windows Machine, you will then need to go into the VM, Disk Management, and extend the drive inside the Windows operating system.


# Content Library

## Add Files to the Content Library

* Log into vCenter
* You should default to the Hosts and Clusters view
* Hover over home button at the top of the screen
* Select Content Library
* Select the Content Library you want to add files to
* Select the Other Types tab – Here you will see the current ISO’s loaded
* Select Import Item
* Select the radio button next to Local File
* Give the item a name
* Select OK

# Remote Console

## Install the Remote Console Viewer

* Log into vCenter
* You should default to the Hosts and Clusters view
* Expand the cluster if needed
* Left click on any virtual machine and open the Summary tab
* In the screenshot for the machine, select the Gear 
* Select Install Remote Console

## Remote Console into a virtual machine

* Log into vCenter
* You should default to the Hosts and Clusters view
* Expand the cluster if needed
* Right Click the virtual machine
* Select Open Console

## Change the Default Console Viewer

You have the option to either use the console in the browser or the remote console viewer. This is how you can switch between the two.

* Log into vCenter
* You should default to the Hosts and Clusters view
* Expand the cluster if needed
* Left click on any virtual machine and open the Summary tab
* In the screenshot for the machine, select the Gear
* Select Change Default Console
* Select the console mode you would prefer to use
* Select OK

# vMotion

If you need to move a VM across hosts manually. If this is completed with the same connected storage, VM’s can remain in a live state. If changing storage connections, the VM’s will need to be powered down and a Host and Storage vMotion will need to occur.

* Log into vCenter 
* You should default to the Hosts and Clusters view
* Expand the cluster if needed
* Right click the desired machine
* Select Migrate
* Select Change compute resource only
* Select Next
* Select the Host you would like to migrate to
* Select Next
* Address any errors that pop up
* Select Next
* Select Finish
* Wait for the process to complete

![](/assets/vmware-vmotion.png)

# Updates and Upgrades

## Updating vCenter

### Manual

* Download patch ISO from [https://my.vmware.com/group/vmware/patch\#search](https://my.vmware.com/group/vmware/patch#search) 
* Remote into host hosting vcenter \(not vcenter itself\) 
* Power off vcenter 
* Take a snapshot of vCenter \(must be completed when vcenter is powered off - this is why connecting to host is important\) 
* Turn on vCenter 
* Wait an extended time for vCenter services to start 
* Load supported patch ISO onto vCenter Appliance 
* Run the following command

```text
software-packages stage --iso 
```

* Hit enter to go through the EULA 
* Type yes at the end 
* Run the following command to view the loaded patches and supported builds to upgrade from 

```text
software-packages list --staged
```

* Run the following command to install the patches

```text
software-packages install --staged 
```

* After install, it will prompt you to reboot. Run the following to reboot

```text
shutdown reboot –r Update_to_last_patches
```

### Web GUI

[https://vmarena.com/how-to-update-patch-vmware-vcenter-server-appliance-vcsa-6-7-offline/](https://vmarena.com/how-to-update-patch-vmware-vcenter-server-appliance-vcsa-6-7-offline/)

* Log in to the VAMI web GUI at [https://vcenterFQDN.example.com:5480](https://vcenterFQDN.example.com:5480) 
* Select Update 
* Select Check updates on right side of screen

## Updating vSphere

### Nutanix

#### Download the latest OEM specific vmware patch

* Log into my.vmware.com 
* Select Products 
* Select All Products and Programs 
* Select All Products 
* Find VMWare VSphere 
* Select View Download Components 
* Select the VSphere version you would like to download \(6.5, 6.7, 7.0, etc.\) 
* Select Custom ISOs & Addons 
* Open the OEM Customized Installer CD's 
* Select the download next to the latest OEM update you are looking for 
* Locate the ZIP file and download it 
* Select the more button next to the zip file, scroll to the bottom, and copy the MD5 checksum to a notepad 

#### Trigger upgrade in PRISM \(Assuming AOS is updated\) 

* Log into PRISM 
* Select the gear at the top right 
* Go to Upgrade Software 
* Select Hypervisor 
* Select  **Upload hypervisor binary?**  
* Locate the ZIP file and paste the MD5 checksum 
* Run a upgrade precheck
  * If it says there is a CD-ROM loaded, there is probably a Nutanix Guest Tools or VM Guest Tools mounted inside of Prism, go to the VM menu, select the VM in question, Manage Guest Tools, and unmount NGT and VMWare Guest Tools. 
* When the precheck succeeds, proceed with the upgrade. This will take an extended amount of time.

