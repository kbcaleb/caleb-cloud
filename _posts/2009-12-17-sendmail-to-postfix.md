---
title: Sendmail to Postfix
date: 2009-12-17 11:27:25.000000000 -07:00
categories:
  - mail
tags:
  - mail
header:
  teaser: "/assets/images/mail.jpeg"
  show_overlay_excerpt: false
---
Stop your current MTA
```shell
service sendmail stop
```
Install Postfix
```shell
yum install postfix
```
Set Postfix to be new MTA
```shell
alternatives --set mta /usr/sbin/sendmail.postfix &amp;&amp; service postfix start
```
Verify you get the Postfix agent
```shell
telnet youromdian.com 25
```
You are looking for the Postfix line like this
```shell
220 your.domain.com ESMTP Postfix
```
