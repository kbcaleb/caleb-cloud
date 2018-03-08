---
title: Apache proxy to a different port
date: 2014-08-26 11:31:41.000000000 -06:00
categories:
  - apache
tags:
  - apache
---
Sometimes you may need to redirect a simple URL like jira.company.com to something like jira.company.com:8080 for easier access. A simple Apache Proxy will solve this.
```apache
<VirtualHost *:80>
ServerName yourdomain.com
ProxyPass / http://yourdomain:8080
ProxyReverse / http://yourdomain.com
```
