---
layout: default
title: SPF
parent: DNS

---
# Sender Policy Framework \(SPF\)
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## TLDR

SPF allows you to define what servers/IP addresses are allowed to send emails for your domain.

## How It Works

SPF uses a TXT DNS record to authenticate allowed email sending servers on your domain. When email is sent, the receiving server pulls the TXT DNS records of the domain located in the ENVELOPE FROM header of the email. If a SPF record is found in the TXT DNS record, it checks the allowed servers/IP's with those allowed in the SPF record. If an email does not pass SPF, it can either be SOFTFAIL'ed \(receiving servers can allow softfail if desired and mark as an SPF failure\), or can be FAILED completely.

### Example

A message is sent From emailserver.example.com \(192.168.1.250\) To testemail@example.org. The example.ORG server checks the DNS TXT records of the domain found in the Envelope Fom \(example.com\) for SPF. If one is found, example.org checks the SPF record to see if the sending IP address of the message is listed in the allowed servers for example.COM. 

If the server is included, the message passes. If it does not match, it follows the requested behavior of both the owner of the sending domain and the policies of the recipient's filters.

> **NOTE:** I intentionally included an unroutable IP address for this example. For your SPF records, you will be using publicly routable IP addresses

## How It Is Set Up

### DNS Location

A SPF TXT record that is externally viewable is located on the domain or subdomain that will be attached to the ENVELOPE FROM - generally on the same domain as your mail server.

**You can only have one SPF TXT record on your domain.**

### Common Mechanisms

You can use a combination of mechanisms to add records.

| Mechanism | Purpose |
| :--- | :--- |
| **v=spf1** | Located at the beginning of an SPF record |
| **A** | Use the A record for that domain or subdomain |
| **MX** | Use the MX records for that domain or subdomain |
| **IP4** | Use an IP4 address \(ip4:1.1.1.1\) |
| **IP6** | Use an IP6 address |
| **INCLUDE** | Use the SPF records found at this domain |
| **-ALL** | FAIL all emails that do not pass the other mechanisms \(Can not be used with SOFTFAIL\) |
| **~ALL** | SOFTFAIL all emails that do not pass the other mechanisms \(Can not be used with FAIL\) |

### Example

 v=spf1 a mx ip4:192.168.1.250 include:\_spf.google.com -all

> **NOTE:** I intentionally included an unroutable IP address for this example. For your SPF records, you will be using publicly routable IP addresses

### Limits

The limit of DNS lookups an SPF record can have is ten. the "all", "ip4" and "ip6" mechanisms do not count against this limit as they do not require a DNS lookup request.

## Reference:

### RFC 7208 

{% embed url="https://tools.ietf.org/html/rfc7208" %}



