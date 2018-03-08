---
title: Deny certain browsers access to a module
date: 2007-11-21 11:26:01.000000000 -07:00
categories:
  - apache
tags:
  - apache
header:
  teaser: "/assets/images/security.png"
  show_overlay_excerpt: false
---
Add the following to your httpd.conf for VirtualHost.

```apache
BrowserMatch "^Browser/ver#" no-modulename
```
