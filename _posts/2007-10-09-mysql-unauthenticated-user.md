---
title: MySQL unauthenticated user
date: 2007-10-09 11:08:32.000000000 -06:00
categories:
  - mysql
tags:
  - mysql
header:
  teaser: "/assets/images/mysql.png"
  show_overlay_excerpt: false
---
Often time you will see stacked MySQL queries with the listing of "unauthenticated user". This is a known bug in MySQL right now where it cannot perform a valid reverse DNS lookup. This will cause the queries to stack and hang sometimes. If you need to get by this bug you can disable DNS lookups which will also help performance. Just add the following to your /etc/my.cnf file.

```sql
skip-name-resolve
```
