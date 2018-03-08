---
title: Grant sudo access to group with no password
date: 2014-08-26 11:31:17.000000000 -06:00
categories:
  - sudo
tags:
  - sudo
header:
  teaser: "/assets/images/sudo.jpeg"
  show_overlay_excerpt: false
---
While I am not a fan of this setup sometimes there is a special request and it needs to be setup.

```shell
visudo
```

Now add a line for the group you are going to setup
```shell
%yourgroupname ALL=(ALL) NOPASSWD: ALL
```
