---
layout: default
title: Grafana Loki
parent: Log Aggregation
---

# Grafana Loki
{: .no_toc }

Low-Index Log Aggregation by Grafana
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

* TOC
{:toc}

---

# Install

## Docker

### Pre-requisites
* Docker
* Git

### Set-Up
```
git clone https://github.com/grafana/loki.git
cd loki/production
sudo docker-compose pull
sudo docker-compose up
```