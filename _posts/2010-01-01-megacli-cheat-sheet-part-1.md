---
title: MegaCLI cheat sheet part 1
date: 2010-01-01 11:29:17.000000000 -07:00
categories:
  - storage
tags:
  - storage
header:
  teaser: "/assets/images/RAID.jpg"
  show_overlay_excerpt: false
---
Here are some quick commands that I have to use on a daily basis for  RAID automation issues. You can either keep -aall in there or if you  have more then one adapter you can replace -aall with the actual adapter  number such as -a0 and you could replace -lall with you actual logical  drive number like -l0.
Get basic adapter information including Adapter#
```shell
MegaCli -adpallinfo -aall
```
List all physical disk information
```shell
MegaCli -pdlist -aall

```
Show information about a particular disk<br />
(replace 252 with you enclosure ID and 4 with the drive ID)
```shell
MegaCli -pdinfo -physdrv [252:4] -aall

```
Show logical drive information and status
```shell
Megacli -ldinfo -lall -aall

```
Start logical drive consistency check
```shell
MegaCli -ldcc -start -lall -aall

```
View progress of consistency check
```shell
MegaCli -ldcc -showprog -lall -aall

```
Get SAS Enclosure information
```shell
MegaCli -encinfo -aall

```
Show all BBU information
```shell
MegaCli -adpbbucmd -aall

```
Show patrol read information
```shell
MegaCli -adppr -info -aall

```
Start a patrol read
```shell
MegaCli -adppr -start -aall

```
View progress of patrol read
```shell
Megacli -adppr -info -aall

```
Enable/Disable alarm
```shell
MegaCli -adpsetprop alarmdsbl -aall
MegaCli -adpsetprop alarmenbl -aall

```
View current log
```shell
MegaCli -fwtermlog -dsply -aall

```
Dump event log to file for checking
```shell
MegaCli -adpeventlog -getevents -f /tmp/event.log -a0

```
