---
title: Change a MySQL database charset
date: 2007-10-05 11:08:00.000000000 -06:00
categories:
  - mysql
tags:
  - mysql
header:
  teaser: "/assets/images/mysql.png"
  show_overlay_excerpt: false
---
Sometime you may need to change your database to use a different charset. Just issue the following from a MySQL prompt.

```sql
ALTER DATABASE dbname CHARSET utf8;
```
