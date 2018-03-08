---
title: Change to stronger SHA-512 passwords for system
date: 2009-12-21 11:28:09.000000000 -07:00
categories:
  - linux
tags:
  - linux
header:
  teaser: "/assets/images/sha512.png"
  show_overlay_excerpt: false
---
I want to set a requirement of at least 1 uppercase, 1 lowercaser, 1  number, & 1 special character. First we will modify  /etc/pam.d/system-auth and change the following line.
```shell
password requisite pam_cracklib.so try_first_pass retry=3
```
to
```shell
password required try_first_pass retry=3 minlen=14 dcredit=-1 ucredit=-1 ocredit=-1 lcredit=0
```
Now we are going to set a lockout for failed passwords by changing.
```shell
auth sufficient pam_unix.so nullok try_first_pass
```
to
```shell
auth required pam_unix.so nullok try_first_pass
```
Now comment out the following 2 lines
```shell
auth requisite pam_succeed_if.so uid &gt;= 500 quiet
auth required pam_deny.so
```
Now add the following to the end of the auth lines in the /etc/pam.d/sshd file
```shell
auth required pam_tally2.so deny=5 onerr=fail
```
And this to the end of the the account lines
```shell
account required pam_tally2.so
```
If you get any accounts locked out you can use this to unlock them
```shell
/sbin/pam_tally2 --user username --reset
```
Now lets set the password hashing algorithm to SHA-512
```shell
authconfig --passalgo=SHA512 --update
```
Now reset the password for all your users. You can cat the  /etc/shadow file and verify the passwords start with $5  now instead of  $1
