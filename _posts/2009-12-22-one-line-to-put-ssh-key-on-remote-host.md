---
title: One line to put SSH key on remote host
date: 2009-12-22 11:28:52.000000000 -07:00
categories:
  - ssh
tags:
  - ssh
header:
  teaser: "/assets/images/ssh.jpeg"
  show_overlay_excerpt: false
---
```shell
cat ~/.ssh/id_rsa.pub | ssh user@hostname 'cat >> .ssh/authorized_keys'
```
or
```shell
ssh-copy-id user@host
```
