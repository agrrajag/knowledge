---
layout: default
title: Microsoft KMS
parent: Volume Licensing
---


# Microsoft Key Management Service \(KMS\)
{: .no_toc }

Volume Activation for Microsoft Products
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

* TOC
{:toc}

---

> **NOTE\:** KMS Activations have a limited \'grace period\' where they are able to hold activation without checking in with the KMS Server. If the machine falls out of the grace period, you will need to connect back to the network with the KMS server, login, and potentially run gpupdate. 

## Activate a Product

KMS Activations require the server KMS is running on to be updated with the latest updates. It is updated through Windows Update. Before you start a KMS Activation, ensure it has received the latest Windows Updates.

* Remote in to your KMS Server
* If you have been provided a Key Management Host program, install that after the latest Windows Updates
* Select Start
* Right Click Volume Activation Tools
* Run as an Administrator
* Select Next
* Select the radio button next to Key Management Service
* Type the name of the KMS server
* Select Next
* Select Install Your KMS Host Key
* Paste Key
* Select Commit
* Proceed through any additional prompts that may pop up to activate.

