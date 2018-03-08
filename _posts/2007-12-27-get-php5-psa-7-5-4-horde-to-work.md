---
title: Get PHP5, PSA 7.5.4, & Horde to work
date: 2007-12-27 11:23:07.000000000 -07:00
categories:
  - plesj
tags:
  - plesk
header:
  teaser: "/assets/images/plesk.png"
  show_overlay_excerpt: false
---
You will need to perform the following to allow Horde on PSA 7.5.4 to work with PHP5.
```shell
pear upgrade DB
cp /usr/share/pear/DB.php /usr/share/psa-horde/pear/DB.php
cp /usr/share/pear/DB/ /usr/share/psa-horde/pear/DB/
```
