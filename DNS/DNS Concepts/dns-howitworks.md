---
layout: default
title: How It Works
grand_parent: DNS
parent: DNS Concepts

---
# How DNS Works
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

* TOC
{:toc}

---

# How It Works

**Taken from** [https://dyn.com/blog/dns-why-its-important-how-it-works/](https://dyn.com/blog/dns-why-its-important-how-it-works/)

> When you visit a domain such as dyn.com, your computer follows a series of steps to turn the human-readable web address into a machine-readable IP address. This happens every time you use a domain name, whether you are viewing websites, sending email or listening to Internet radio stations like Pandora.
>
> ## Step 1: Request information
>
> The process begins when you ask your computer to resolve a hostname, such as visiting [http://dyn.com](http://dyn.com). The first place your computer looks is its local DNS cache, which stores information that your computer has recently retrieved. If your computer doesn’t already know the answer, it needs to perform a DNS query to find out.
>
> ## Step 2: Ask the recursive DNS servers
>
> If the information is not stored locally, your computer queries \(contacts\) your ISP’s recursive DNS servers. These specialized computers perform the legwork of a DNS query on your behalf. Recursive servers have their own caches, so the process usually ends here and the information is returned to the user.
>
> ## Step 3: Ask the root nameservers
>
> If the recursive servers don’t have the answer, they query the root nameservers. A nameserver is a computer that answers questions about domain names, such as IP addresses. The thirteen root nameservers act as a kind of telephone switchboard for DNS. They don’t know the answer, but they can direct our query to someone that knows where to find it.
>
> ## Step 4: Ask the TLD nameservers
>
> The root nameservers will look at the first part of our request, reading from right to left — www.dyn.com — and direct our query to the Top-Level Domain \(TLD\) nameservers for .com. Each TLD, such as .com, .org, and .us, have their own set of nameservers, which act like a receptionist for each TLD. These servers don’t have the information we need, but they can refer us directly to the servers that do have the information.
>
> ## Step 5: Ask the authoritative DNS servers
>
> The TLD nameservers review the next part of our request — www.dyn.com — and direct our query to the nameservers responsible for this specific domain. These authoritative nameservers are responsible for knowing all the information about a specific domain, which are stored in DNS records. There are many types of records, which each contain a different kind of information. In this example, we want to know the IP address for www.dyndns.com, so we ask the authoritative nameserver for the Address Record \(A\).
>
> ## Step 6: Retrieve the record
>
> The recursive server retrieves the A record for dyn.com from the authoritative nameservers and stores the record in its local cache. If anyone else requests the host record for dyn.com, the recursive servers will already have the answer and will not need to go through the lookup process again. All records have a time-to-live value, which is like an expiration date. After a while, the recursive server will need to ask for a new copy of the record to make sure the information doesn’t become out-of-date.
>
> ## Step 7: Receive the answer
>
> Armed with the answer, recursive server returns the A record back to your computer. Your computer stores the record in its cache, reads the IP address from the record, then passes this information to your browser. The browser then opens a connection to the webserver and receives the website.
>
> **This entire process, from start to finish, takes only milliseconds to complete.**

# Types of DNS Records

| Record | Purpose |
| :--- | :--- |
| **A** | Converts domain to IPv4 address – google.com A 172.217.9.206 |
| **AAAA** | Converts domain to IPv6 address – google.com AAAA 2607:f8b0:4006:811::200e |
| **CNAME** | Points domain to another domain – www.google.com CNAME forcesafesearch.google.com |
| **DNAME** | Points domain to another domain – www.google.com DNAME forcesafesearch.google.com |
| **MX** | Determines Mail Flow For Domain by Priority – example.com MX 10 mail.example.com |
| **NS** | Specify alternative authoritative DNS server – hosted.example.com NS ns-cloud-b1.googledomains.com |
| **PTR** | Converts IPv4 address to domain for verification - 172.217.9.206 PTR google.com |
| **SOA** | Specifies core information about DNS zone – computer1.example.com SOA dc.example.com |
| **TXT** | Random information needed for DNS-based validation checks |