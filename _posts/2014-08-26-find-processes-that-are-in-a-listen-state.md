---
title: Find processes that are in a LISTEN state
date: 2014-08-26 11:33:01.000000000 -06:00
categories:
  - network
tags:
  - network
header:
  teaser: "/assets/images/security.png"
  show_overlay_excerpt: false
---
I just use a lsof to pull the network stack and then look for LISTEN status
```shell
lsof -n | grep LISTEN
```
