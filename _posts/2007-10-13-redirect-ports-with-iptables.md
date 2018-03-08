---
title: Redirect ports with IPtables
date: 2007-10-13 11:10:51.000000000 -06:00
status: publish
categories:
  - firewall
tags:
  - firewall
header:
  teaser: "/assets/images/firewall.png"
  show_overlay_excerpt: false
---
For whatever reason you may want to remap a high port to a low port. Here is how you can do it with IPtables. In this example we are going to remap 23420 to port 25 on IP address 192.168.1.1.

```shell
iptables -t nat -A PREROUTING -p tcp --dport 23420 -j DNAT --to 192.168.1.1:25
```
