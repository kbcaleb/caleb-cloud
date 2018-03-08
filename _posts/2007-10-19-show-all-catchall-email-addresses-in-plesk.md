---
title: Show all catchall email addresses in Plesk
date: 2007-10-19 11:12:09.000000000 -06:00
categories:
  - plesk
tags:
  - plesk
header:
  teaser: "/assets/images/spam.png"
  show_overlay_excerpt: false
---
These need to be monitored because all to often domains with these catch alls are used as SPAM reply to addresses in email.

```sql
select d.name as domain, p.value as catchall_address from Parameters p, DomainServices ds, domains d where d.id = ds.dom_id and ds.parameters_id = p.id and p.parameter = 'catch_addr' order by d.name;
```
