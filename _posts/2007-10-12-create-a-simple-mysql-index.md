---
title: Create a simple MySQL index
date: 2007-10-12 11:10:04.000000000 -06:00
categories:
  - mysql
tags:
  - mysql
header:
  teaser: "/assets/images/mysql.png"
  show_overlay_excerpt: false
---
Here is how you can create a MySQL index. Be aware of where you are using indexes they can be just as beneficial as they can be disastrous to performance.

```sql
ALTER TABLE table_name ADD INDEX index_name (field1, field2);
```
