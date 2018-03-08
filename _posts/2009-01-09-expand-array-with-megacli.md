---
title: Expand array with MegaCLI
date: 2009-01-09 11:26:58.000000000 -07:00
categories:
  - storage
tags:
  - storage
header:
  teaser: "/assets/images/RAID.jpg"
  show_overlay_excerpt: false
---
Recently I needed to add 2 more 1tb drives to my current RAID5 x3 1TB  setup. This was all done with a hotswap cage and no downtime. I will  show you how I added the first one in this example enclosure(252)  slot(2).
Clear it
```shell
MegaCli -pdclear -start -physdrv '[252:2]' -a0
```
Set state to (Unconfigured Good)
```shell
MegaCli -pdmakegood -physdrv '[252:2]' -a0
```
Add to current logical volume
```shell
MegaCli -ldrecon -start -add -physdrv '[252:2]' -l0 -a0
```
Check Progress sigh…
```shell
MegaCli -ldrecon -showprog -l0 -a0
```
Prepare for a pretty long wait if you have a large array.
```shell
Reconstruction on VD #0 (target id #0) Completed 43% in 501 Minutes.
```
and this is for a 1.8TB with and additional 1TB drive being added to the array.
```shell
/dev/mapper/vg0-lvol0 1.8T 1.6G 1.8T 1% /media/pub
```
Yeah!
