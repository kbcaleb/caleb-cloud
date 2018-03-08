---
title: Mount ISO as a loopback device
date: 2014-08-24 11:32:06.000000000 -06:00
categories:
  - storage
tags:
  - storage
header:
  teaser: "/assets/images/iso.jpg"
  show_overlay_excerpt: false
---
Mount a ISO file as a loopback device for access.
```shell
cd /path/to/dir/with/ISO
mount yourfile.iso -o loop /mnt
```
