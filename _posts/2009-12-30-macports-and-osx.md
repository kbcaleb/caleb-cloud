---
title: MacPorts and osX
date: 2009-12-30 11:30:11.000000000 -07:00
categories:
  - mac
tags:
  - mac
header:
  teaser: "/assets/images/win7.jpeg"
  show_overlay_excerpt: false
---
Install a port
```shell
port install port_name
```
Install pre-compiled binary port
```shell
port pkg port_name
```
Create osX DMG file from port
```shell
port dmg port_name
```
Create RPM file from port
```shell
port rpm port_name
```
Upgrade a port
```shell
port upgrade port_name
```
Upgrade all outdated ports
```shell
port upgrade outdated
```
Upgrade a port but not the dependencies
```shell
port -n upgrade port_name
```
Upgrade a port and uninstall the old version
```shell
port -u upgrade port_name
```
Uninstall a port (You can force with -f)
```shell
port uninstall port_name
```
Uninstall all ports
```shell
port uninstall all
```
Clean a port
```shell
>port clean --all port_name
```
List port contents
```shell
port contents port_name
```
List all ports
```shell
port list
```
List all installed ports
```shell
port installed
```
List outdated ports
```shell
port outdated
```
Search ports
```shell
port search whatever
```
Port info
```shell
port info port_name
```
Show port dependencies
```shell
port deps port_name
```
Show port variants
```shell
port variants port_name
```
Invoking variants for ports
```shell
port install port_name +variant_name
```
Removing default variants
```shell
port install port_name -variant_name
```
