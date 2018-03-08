---
title: Non-static method PMA_Config::isHttps() should not be called statically
date: 2007-01-20 11:01:12.000000000 -07:00
categories:
  - plesk
tags:
  - plesk
header:
  teaser: "/assets/images/plesk.png"
  show_overlay_excerpt: false
---
This looks worse then it really is in plesk. The password in the PSA DB does not match the one set for the user in mysql.user. Just reset the password in the control panel for that DB user to correct it.

```shell
Non-static method PMA_Config::isHttps() should not be called statically
```
