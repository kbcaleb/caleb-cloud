---
title: Rewrite Non-SSL to SSL
date: 2007-10-08 11:03:51.000000000 -06:00
categories:
  - ssl
tags:
  - ssl
header:
  teaser: "/assets/images/ssl.png"
  show_overlay_excerpt: false
---
Simple rewrite rule to send all HTTP requests for any URL to a HTTPS connection.

```apache
RewriteEngine on
RewriteCond %{SERVER_PORT} =80
RewriteRule ^(.*) https://%{SERVER_NAME}%{REQUEST_URI}
```
