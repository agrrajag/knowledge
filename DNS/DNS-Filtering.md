---
layout: default
title: Filtering
parent: DNS

---
# DNS Filtering
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Forward Lookups and CIPA/HTTPS DNS Strategies

CIPA requires strict internet filtering when delivering service to students. With the push to secure the web, traditional filtering methods had issues filtering search results. Search providers have come up with new ways to force safe search at a DNS level instead of through a traditional MITM filter.

To complete this, we set up forward lookup zones for the different search providers that allow this service.

| Bing | Google | Youtube |
| :--- | :--- | :--- |
| FLZ: www.bing.com | FLZ: www.google.com | FLZ: www.youtube.com |
| A: 204.79.197.220 | A: 216.239.38.120 | FLZ: m.youtube.com |
| DNAME: strict.bing.com. | DNAME: forcesafesearch.google.com. | FLZ: www.youtube-nocookie.com |
|  |  | FLZ: youtube.googleapis.com |
|  |  | FLZ: youtubei.googleapis.com |
|  |  | A: 216.239.38.119 |

