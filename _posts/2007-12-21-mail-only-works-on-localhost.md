---
title: Mail only works on localhost
date: 2007-12-21 11:24:03.000000000 -07:00
categories:
  - mail
tags:
  - mail
header:
  teaser: "/assets/images/spam.png"
  show_overlay_excerpt: false
---
This happens quite often with new users or admins who are not familiar with mail setups.
Postfix (/etc/postfix/main.cf

```shell
inet_interfaces = localhost
```
Change to

```shell
inet_interfaces = all
```
Sendmail (/etc/mail/sendmail.mc

```shell
DAEMON_OPTIONS('Port=smtp,Addr=127.0.0.1, Name=MTA')dnl
```
Change to

```shell
DAEMON_OPTIONS('Port=smtp,Addr=0.0.0.0, Name=MTA')dnl
```

Services need to be notified of the changes
```shell
sendmail service restart
```

or
```shell
service postfix reload
```
