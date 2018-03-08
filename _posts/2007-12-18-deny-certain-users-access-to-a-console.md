---
title: Deny certain users access to a console
date: 2007-12-18 11:24:46.000000000 -07:00
categories:
  - security
tags:
  - security
header:
  teaser: "/assets/images/security.png"
  show_overlay_excerpt: false
---
Add the required pam_access line to your system-auth or login file in the /etc/pam.d directory. This needs to be the first auth line to override the previous one.

```shell
auth required pam_access.so
```
Now add the following to the /etc/security/access.conf file.

```shell
-:username:tty#
```
