---
title: Show MySQL queries in real time
date: 2008-01-17 11:21:23.000000000 -07:00
categories:
  - mysql
tags:
  - mysql
header:
  teaser: "/assets/images/mysql.png"
  show_overlay_excerpt: false
---
Here is a quick one line to allow you to watch current MySQL queries.
```shell
mysqladmin -vi 1 proc
```
