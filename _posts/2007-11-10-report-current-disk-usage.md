---
title: Report current disk usage
date: 2007-11-10 11:13:52.000000000 -07:00
categories:
  - storage
tags:
  - storage
header:
  teaser: "/assets/images/disk.jpg"
  show_overlay_excerpt: false
---
This is good for trying to chase down which directories are eating up the most space and give you a file with the report sorted by size in MB.

```shell
( du -SB 1M / | sort -grk 1 ) > disk_usage.txt 2&> /dev/null
```
