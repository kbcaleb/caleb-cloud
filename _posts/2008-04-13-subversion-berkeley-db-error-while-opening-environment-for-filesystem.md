---
title: Subversion Berkeley DB error while opening environment for filesystem
date: 2008-04-13 11:17:34.000000000 -06:00
categories:
  - svn
tags:
  - svn
---
This seems to be caused by versions before 1.4.3 because of the  difference in the set fstype for create. To correct this problem you  need to specify the correct fstype when making the svn repo.
```shell
svnadmin create /path/to/svn/repo --fs-type fsfs
```
