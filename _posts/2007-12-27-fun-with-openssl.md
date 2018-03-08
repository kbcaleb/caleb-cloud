---
title: Fun with OpenSSL
date: 2007-12-27 11:22:38.000000000 -07:00
categories:
  - ssl
tags:
  - ssl
header:
  teaser: "/assets/images/ssl.png"
  show_overlay_excerpt: false
---
Here are some quick one liners to do a laundry list of things with openssl.
```shell
openssl s_client -connect domain.com:443
```
or for more info
```shell
openssl s_client -state -verify -showcerts -connect domain.com:443
```
Check speed for SSL methods
```shell
openssl speed
openssl speed rsa
```
for SMPopenssl speed rsa -multi 2<br />
Check connection time
```shell
openssl s_time -connect remote.host:443
```
Check SMTP/TLS
```shell
openssl s_client -connect remote.host:25 -starttls smtp
```
Base 64 encoding<br />
send encoded contents of file.txt to stdout
```shell
openssl enc -base64 -in file.txt
```
same, but write contents to file.txt.enc
```shell
openssl enc -base64 -in file.txt -out file.txt.enc
```
Diagnose SSL error codes
```shell
sshd[31784]: error: RSA_public_decrypt failed: error:0407006A:lib(4):func(112):reason(106)
openssl errstr 0407006A
```
Generate crypt style hash
```shell
openssl passwd MySecret
```
Generate shadow style hash
```shell
openssl passwd -1 MySecret
```
with salt
```shell
openssl passwd -1 -salt sXiKzkus MySecret
```
Test for prime numbers
```shell
openssl prime 119054759245460753
```
