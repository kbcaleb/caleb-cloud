---
title: Check for DoS or DDoS connections
date: 2007-10-12 11:09:38.000000000 -06:00
categories:
  - security
tags:
  - security
header:
  teaser: "/assets/images/ddos.png"
  show_overlay_excerpt: false
---
This is just a quick snippet to see what is going on with connection on your server. We are checking port 80 in this example but you can replace 80 with whatever port you are checking.

```shell
netstat -ant | grep \:80 | awk '{ print $5 }' | awk -F \: '{ print $1 }' | sort | uniq -c | sort -n
```
