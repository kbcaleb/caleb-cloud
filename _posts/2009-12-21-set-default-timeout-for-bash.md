---
title: Set default timeout for bash
date: 2009-12-21 11:27:46.000000000 -07:00
categories:
  - linux
tags:
  - linux
header:
  teaser: "/assets/images/shell.jpg"
  show_overlay_excerpt: false
---
Create the following in the /etc/profile.d/tmout.sh
```shell
TMOUT=900
readonly TMOUT
export TMOUT
```
Now chmod 755 that file and your good to go.
