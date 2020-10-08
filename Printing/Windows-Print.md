---
layout: default
parent: Printing
title: Windows Print Services
has_children: true
---

# Windows Print Services

## Table of contents
{: .no_toc .text-delta }


* TOC
{:toc}

---
# Microsoft Print Server

## Adding a Printer to the Print Server
> NOTE: Make sure the printer has either a static IP address or you have set a [DHCP Reserved Address](https://knowledge.ryangarr.com/DHCP/MS-DHCP.html#setting-the-dhcp-reserved-address-if-not-already-assigned)

* Confirm IP settings and model information is correct
* RDP into the print server you would like to add the printer to
* Open the Print Management application
* Expand Print Servers
* Expand the name of the server
* Select Printers
* Right Click Printers
* Select Add Printer
* Select Add a TCP/IP or Web Services Printer by IP address or hostname
* Select Next
* Change Type of Device to TCI/IP device
* Type or Paste the IP address where it says Host Name or IP address
* You can leave Auto detect the printer driver selected
* Port Name will auto-populate
    * If an underscore number pops up after the IP address on the Port Name, the IP address already has a port associated with it. Use the following steps to use the existing port:
        * Select Back
        * Select Add a new printer using an existing port
        * Use the drop down to locate the correct IP address
* Select Next
    * If it has detected the correct printer driver, it will skip directly to the naming segment. It will only auto-detect specific model printer drivers we have loaded that the universal drivers were not compatible with.
* Select the correct printer driver – usually a versioned universal one 
* Select Next
* Name the printer
* Leave Share this Printer selected
* Change Share Name to be the same as the Printer Name
* Select Next
* Select Next again to confirm the changes on the screen
* Once it is installed, it will give you a confirmation. You can use this to print a test page as well.
