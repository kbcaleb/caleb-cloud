---
title: Change MySQL open file limit
date: 2007-10-10 11:09:11.000000000 -06:00
categories:
  - mysql
tags:
  - mysql
header:
  teaser: "/assets/images/mysql.png"
  show_overlay_excerpt: false
---
This one used to get new techs because they would see the error message and think the file limit error was pertaining to the kernel and not MySQL. You can add the following to the /etc/my.cnf to change the value.

```sql
open_file_limit=1400
```
