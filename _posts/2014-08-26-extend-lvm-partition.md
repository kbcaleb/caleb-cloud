---
title: Extend LVM partition
date: 2014-08-26 11:33:22.000000000 -06:00
categories:
  - storage
tags:
  - storage
header:
  teaser: "/assets/images/lvm.png"
  show_overlay_excerpt: false
---
This is really easy and is something every linux admin should know. In this example we are going to extend it to be 500MB. If I wanted to add 500MB then I would have used the + sign for L+500M.
```shell
umount /path/to/you/partition
lvextend /path/to/your/partition -L500M
e2fsck -f /path/to/your/partition
resize2fs /path/to/your/partition
mount /path/to/your/partition

```
Verify the extra space is there and you are good to go.
