---
layout: default
title: DMARC
grand_parent: DNS
parent: DNS Concepts

---
# Domain-based Message Authentication, Reporting and Conformance \(DMARC\)
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

* TOC
{:toc}

---

# TLDR

DMARC sets up policies for who can send emails on your domain's behalf based on DKIM and SPF. This allows you to set specific rules when messages fail, and also receives reports back from major email carriers.

# How It Works

After you have SPF and DKIM set up on your domain, you can use DMARC to further set up pDMARC works as a TXT DNS entry set up on a specific subdomain: **\_dmarc**.example.com. The mechanisms added to the DNS define the policy. DMARC takes action and performs the "**p="** policy action when an email fails either SPF or DKIM. 

# How It Is Set Up

## Typical DMARC mechanisms

| Mechanism | Purpose |
| :--- | :--- |
| **v=DMARC1** | Located at the beginning of a DMARC record |
| **p=** | Determines policy response. Can be none, quarantine, or reject  |
| **rua=mailto:** | Tells the receiving server what email to send aggregate reports of DMARC failures |
| **ruf=mailto:** | Tells the receiving server what email to send forensic reports of DMARC failures |
| **rf=** | Tells what kind of report the policyholder wants delivered. **afrf** is default |
| **pct=100** | Tells the receiving server what percent of the mail was subject to the DMARC policy. |
| **sp=** | Determines if policy applies to subdomains. **none** is default |
| **adkim=** | DMARC strict or relaxed - **r** is default |
| **aspf=** | SPF strict or relaxed - **r** is default |

## Example DNS Record

### **\_dmarc**.example.com

"v=DMARC1; p=reject; pct=100; rua=mailto:dmarc@example.com; sp=none; aspf=r;"

# Resources

## Free DMARC Aggregator and Report Generator

[https://dmarc.postmarkapp.com](https://dmarc.postmarkapp.com)



