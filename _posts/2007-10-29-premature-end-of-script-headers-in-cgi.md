---
title: Premature end of script headers in CGI
date: 2007-10-29 11:12:57.000000000 -06:00
categories:
  - apache
tags:
  - apache
header:
  teaser: "/assets/images/security.png"
  show_overlay_excerpt: false
---
This is old but still comes up sometimes. Make sure the script is 755 and the file is in the correct format.<br />
First verify the file is not in binary.

```shell
vi -b filename
```

With plesk with suexec you need to set the uid:gid to the userID for the domain and the psacln group.

```shell
chown userid:psacln file.cgi
```

Now one last think you can do is check the syntax of the file

```shell
perl -c file.cgi
```
