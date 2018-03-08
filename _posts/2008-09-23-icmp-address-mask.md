---
title: ICMP address mask
date: 2008-09-23 11:26:30.000000000 -06:00
categories:
  - network
tags:
  - network
header:
  teaser: "/assets/images/icmp.png"
  show_overlay_excerpt: false
---
So I recently had a customer who needed to have the address mask  reply and request disabled for his server. On linux this sysctl value is  not the same as FreeBSD it actually requires you to convert binary to  decimal.
<code class="lang-markup">icmp_ratemask - INTEGER
        Mask made of ICMP types for which rates are being limited.
        Significant bits: IHGFEDCBA9876543210
        Default mask:     0000001100000011000 (6168)

        Bit definitions (see include/linux/icmp.h):
                0 Echo Reply
                3 Destination Unreachable *
                4 Source Quench *
                5 Redirect
                8 Echo Request
                B Time Exceeded *
                C Parameter Problem *
                D Timestamp Request
                E Timestamp Reply
                F Info Request
                G Info Reply
                H Address Mask Request
                I Address Mask Reply

        * These are rate limited by default (see default mask above)
```
So the current value is 6168 (0000001100000011000) and we are looking  to change the values for H &amp; I which would result in  (1100001100000011000). This is because the H &amp; I are the first 2 in  the mask. Now we can convert it with google calculator to get the  correct new value. Just feed the following into google.
```shell
0b1100001100000011000 in decimal
```
You should then get 399384 which is the value you will set for  net.ipv4.icmp_ratemask. You can do this by adding it to the  /etc/sysctl.conf.
```shell
net.ipv4.icmp_ratemask = 399384
```
