---
title: Check for weak passwords in Plesk mail accounts
date: 2007-10-19 11:12:34.000000000 -06:00
categories:
  - plesk
tags:
  - plesk
header:
  teaser: "/assets/images/plesk.png"
  show_overlay_excerpt: false
---
You can change the password string to some of the more known ones such as 12345, password123, pass123, god, etc..

```sql
select domains.name,domains.id,mail.mail_name,accounts.password from domains,mail,accounts where domains.id=mail.dom_id and accounts.id=mail.account_id and accounts.password='password';
```

And here is the list all for the passwords.
```sql
select CONCAT(mail_name,"@",name) as email_address,accounts.password from mail left join domains on domains.id=mail.dom_id left join accounts on accounts.id=mail.account_id;
```
