---
title: Kill all processes for a user
date: 2007-11-12 11:14:16.000000000 -07:00
categories:
  - security
tags:
  - security
header:
  teaser: "/assets/images/security.png"
  show_overlay_excerpt: false
---
Sometimes you need to kill off any running processes do you can remove a exploited account. Here is a simple quick way.
Using pkill

```shell
pkill -u username
```

And if you do not have pkill you could just do
```shell
ps -o pid -u username | xargs kill -1
```
