---
title: Import a plain CSV file into MySQL
date: 2007-10-14 11:11:44.000000000 -06:00
categories:
  - mysql
tags:
  - mysql
header:
  teaser: "/assets/images/mysql.png"
  show_overlay_excerpt: false
---
This assumes you have already created the required table with all of the correct fields. Also this assumes you are using , as the field separator.

```sql
LOAD DATA INFILE 'filename.txt' INTO table_name FIELDS TERMINATED BY ',';
```
