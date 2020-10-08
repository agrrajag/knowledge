---
layout: default
title: Google Domains
grand_parent: DNS
parent: DNS Management
---
# Google Domains
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

* TOC
{:toc}

---

# Normal DNS records \(A, CNAME, MX, etc.\)

## Creating New Records

* Sign in to domains.google.com
* Locate the domain you would like to modify
* Select the Configure DNS button
* Scroll down to Custom Resource Records
* In the first field, enter the identifier \(subdomain for A, MX, or CNAME; IP for Pointer\)
* In the second field, define the type of record
* Leave TTL at 1H unless directed otherwise
* Enter the reference or value in the last column
* Click Add

![](../../.gitbook/assets/dns-google.png)

## Modifying Existing Records

* Sign in to domains.google.com
* Locate the domain you would like to modify
* Select the Configure DNS button
* Scroll down to Custom Resource Records
* Locate the record you would like to modify
* Select Edit
* Modify the record
* Press Save when complete

# Subdomain Redirects \(301 and 302 redirects\)

Subdomain redirects are used when normal DNS references won’t work. Sometimes receiving servers won't allow you to CNAME to them. Let's also say you want to set up a subdomain redirect in Google so that docs.example.com goes to example.com/docs, but you use a different DNS resolver externally than you do internally. The subdomain would work for everyone except your internal network using the internal resolver. We'll cover both setting up the subdomain redirect on Google and reflecting the change on the internal resolver.

## Setting up the Subdomain Redirect

* Sign in to domains.google.com
* Select Manage on the domain you want to modify
* Select the DNS on the left side
* Scroll down to Synthetic Records
* Create a subdomain forward with the subdomain pointing to the new website
* Determine if it needs temporary or permanent status and do not forward path unless needed
* Enable SSL if desired
* Press Add

> Enabling SSL on a redirect will throw a red error for up to 24 hours while the SSL certificate is generated and applied to the subdomain. There is no need to concern about this

## Adding the Subdomain Redirect to your Internal Resolver

Create a new CNAME record for the desired subdomain on your internal resolver. Point the CNAME to ghs.googlehosted.com.

# Transferring in a domain

## Prerequisites

* Domain must be unlocked
* WHOIS must be public
* Verify registrant contact email
* An authorization code request must have been made
* Domains must be renewed for at least one year at time of transfer \(normally $12\)
* Make a copy of current DNS configuration

> NOTE: If you unlock/make public the domain, it may take up to 20 minutes after the change to reflect in Google Domains

## Transfer In

* Obtain authorization code
* Sign in to Google Domains
* Select Transfer In
* Type in the domain
* It will check if the info is private or locked
* Type in the authorization code
* Select Accept and Proceed
* If you select Detect and import my domain’s current settings, it will run an nslookup on common subdomains – not all subdomains. You can add, edit, and modify these records.
* Select Accept and Proceed to start the transfer and authorize a payment for an additional year of registration
* Confirm contact information and continue
* Select a payment method and continue
* Approve the confirmation email you received
* After you approve the email, it can take up to seven days for a domain to fully transfer.

# Support

For help with Google Domains, you can request a phone call from Google by going to: [https://domains.google.com/contactus](https://domains.google.com/contactus%20)

