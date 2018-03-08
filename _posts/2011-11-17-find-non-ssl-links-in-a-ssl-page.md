---
title: Find Non-SSL links in a SSL page
date: 2011-11-17 11:14:49.000000000 -07:00
categories:
  - ssl
tags:
  - ssl
header:
  teaser: "/assets/images/ssl.png"
  show_overlay_excerpt: false
---
This can help you narrow down certificate warnings about mixed content.
```shell
curl -I domain.com | grep "http:\"
```
