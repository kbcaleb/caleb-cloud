---
title: Redirect traffic to a new IP address
date: 2010-01-15 11:30:55.000000000 -07:00
categories:
  - network
tags:
  - network
header:
  teaser: "/assets/images/firewall.png"
  show_overlay_excerpt: false
---
First make sure you enable forwarding

```shell
sysctl net.ipv4.ip_forward=1
```
Next issue the iptables rules for the port you want to redirect.
```shell
iptables -t nat -A PREROUTING -p tcp --dport 80 -j DNAT --to-destination 69.174.244.190:80
```
Next we will masquerade the traffic
```shell
iptables -t nat -A POSTROUTING -j MASQUERADE
```
Simple
