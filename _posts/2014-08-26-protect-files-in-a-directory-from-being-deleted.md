---
title: Protect files in a directory from being deleted
date: 2014-08-26 11:33:41.000000000 -06:00
categories:
  - linux
tags:
  - linux
header:
  teaser: "/assets/images/protect.jpg"
  show_overlay_excerpt: false
---

Sometimes you may want a shared dropbox folder where users from all over can add files but you do not want them to be able to delete them. This is where you want to look into how ugoa works with permissions for the sticky attribute. By using the sticky attribute on the directory you can prevents unprivileged users from removing or renaming a file in the directory unless the own the file or directory. This is similar to what you would find on the /tmp directory and is referred to as restricted deletion

```shell
mkdir /dropbox
chown root:yourgroup /dropbox
chmod 1777 /dropbox
```
