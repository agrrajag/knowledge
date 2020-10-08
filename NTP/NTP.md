---
layout: default
title: NTP
---

# Network Time Protocol \(NTP\)
{: .no_toc }

Image resolutions for default backgrounds on different IT systems.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

* TOC
{:toc}

---

# Windows Non-Primary Domain Controllers and Workstations

To have computers sync with your primary domain controller, set their source to be the domain hierarchy. This tells workstations to use a domain controller, and domain controllers to use the PDC. You will need to ensure the PDC has an external time source configured.

```
w32tm /config /syncfromflags:DOMHIER /update
w32tm /resync /nowait
net stop w32time
net start w32time
```

## Test Connection to NTP
```
w32tm /monitor
```

## Enable Time Service
```
Net start w32time
```

## Restart Time Service
```
Net stop w32time
Net start w32time
```

# CentOS Linux

```text
sudo nano /etc/ntp.conf
```

> **NOTE:** Find where it says server centos.pool.ntp.gov iburst and switch it to list each domain controller. Save and close the editor