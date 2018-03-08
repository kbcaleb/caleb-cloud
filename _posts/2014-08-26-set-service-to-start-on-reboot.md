---
title: Set service to start on reboot
date: 2014-08-26 11:32:36.000000000 -06:00
categories:
  - redhat
tags:
  - redhat
header:
  teaser: "/assets/images/redhat.jpg"
  show_overlay_excerpt: false
---
Come across this one all the time still. To set a service from init.d to start on reboot you can doo the following.
First list the service that are available and the name of the service you are working with. We will use Apache (httpd) for this example.

```shell
chkconfig --list
```

Now set the service to start on reboots
```shell
chkconfig httpd on
```

You can also set the service to run at various runtimes by using the --level argument.
```shell
chkconfig httpd on --levels 345
```

Or I could set it for only one run level.
```shell
chkconfig httpd on --levels 3
```
