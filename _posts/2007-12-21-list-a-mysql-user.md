---
title: List a MySQL user
date: 2007-12-21 11:25:11.000000000 -07:00
categories:
  - mysql
tags:
  - mysql
header:
  teaser: "/assets/images/mysql.png"
  show_overlay_excerpt: false
---
This one is simple but I get tickets for it all the time.

```sql
select User,Host,Password from mysql.user;
```

You can also do a select all and format it better

```sql
select * from mysql.user\G
```
