---
title: Check for POST spam abuse
date: 2008-01-08 11:22:14.000000000 -07:00
categories:
  - security
tags:
  - security
header:
  teaser: "/assets/images/spam.png"
  show_overlay_excerpt: false
---
Just use a quick 1 liner like this to get some info on what IP has been trying to POST the most and to what script.
```shell
grep POST /home/httpd/vhosts/*/statistics/logs/access_log | awk '{ print $7 }' | sort | uniq -c | sort -nr
```
This can of course be changed to point to your access_logs.
