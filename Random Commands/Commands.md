---
layout: default
title: Helpful Commands
---

# Helpful Commands
{: .no_toc }

Not really sure where else to put these for now...
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

* TOC
{:toc}

---
# Git

## Clean Up Commits
``` git
git checkout --orphan cleanup_branch
git add -A
git commit -am "commit message"
git branch -D master
git branch -m master
git push -f origin master
```

# Windows 

## Find the Serial Number

```
wmic bios get serialnumber
```
