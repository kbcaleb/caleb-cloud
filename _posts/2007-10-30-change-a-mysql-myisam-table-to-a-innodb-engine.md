---
title: Change a MySQL MyISAM table to a InnoDB engine
date: 2007-10-30 11:13:24.000000000 -06:00
categories:
  - mysql
tags:
  - mysql
header:
  teaser: "/assets/images/mysql.png"
  show_overlay_excerpt: false
---
This is easy on smaller tables but on larger ones all data should be backed up first to CYA and changes should be done during off hours to avoid downtime.

```sql
ALTER TABLE 'table_name' ENGINE='InnoDB';
```
