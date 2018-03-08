---
title: Add additional IP addresses to FreeBSD
date: 2007-10-13 11:10:26.000000000 -06:00
categories:
  - FreeBSD
tags:
  - FreeBSD
header:
  teaser: "/assets/images/freebsd.png"
  show_overlay_excerpt: false
---
Here is how you setup a IP alias in FreeBSD. Add the following to your rc.conf file.

```shell
ifconfig_rl0_alias0="192.168.0.57 netmask 255.255.255.255"
```

Now here is the command you can use to bring that interface online instantly.

```shell
ifconfig rl0 alias 192.168.0.57 netmask 255.255.255.255

```
With BSD you use 255.255.255.255 for you IP alias netmasks.
