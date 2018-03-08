---
title: ntpdate – no server suitable for synchronization
date: 2008-03-09 11:18:01.000000000 -06:00
categories:
  - ntp
tags:
  - ntp
---
This is caused by the ntpdate binary not being able to pass data back  because of a firewall or something similar. You can either update the  FW rules or use the -u flag for unprivileged ports.
```shell
ntpdate -u ntp.server.com
```
