---
title: vsftpd with SSL
date: 2008-09-12 11:16:10.000000000 -06:00
categories:
  - vsftpd
tags:
  - vsftpd
---
First lets generate the PEM file.
```shell
openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout /etc/vsftpd/vsftpd.pem -out /etc/vsftpd/vsftpd.pem
```
Now lets add the required entries to the /etc/vsftpd.conf file
```shell

ssl_enable=YES
allow_anon_ssl=NO
force_local_data_ssl=NO
force_local_logins_ssl=NO
ssl_tlsv1=YES
ssl_sslv2=NO
ssl_sslv3=NO
rsa_cert_file=/etc/vsftpd/vsftpd.pem

```
Restart the service and test with <a href="http://fireftp.mozdev.org/">FireFTP</a>
```shell

/etc/rc.d/init.d/vsftpd restart

```
