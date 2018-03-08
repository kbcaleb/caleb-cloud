---
title: Use Xcache 1.21 with Zend Optimizer 3.3.0
date: 2007-11-25 11:25:35.000000000 -07:00
categories:
  - php
tags:
  - php
header:
  teaser: "/assets/images/zend.png"
  show_overlay_excerpt: false
---
The error you get when trying to make this work can be quite deceiving but the real issue is the same that you get in FreeBSD where the module load order can cause problems.

PHP Fatal error: [Zend Optimizer] Zend Optimizer 3.3.0 is incompatible with XCache 1.2.1 in Unknown on line 0

I corrected this by changing the default order of the way Zend loads and loading xcache as a zend_extension.

```shell
[Zend]
zend_extension = /usr/lib/php4/xcache.so
misc xcache flags in between
zend_extension=/usr/local/Zend/lib/ZendExtensionManager.so
zend_extension_ts=/usr/local/Zend/lib/ZendExtensionManager_TS.so
zend_extension_manager.optimizer=/usr/local/Zend/lib/Optimizer-3.3.0
zend_extension_manager.optimizer_ts=/usr/local/Zend/lib/Optimizer_TS-3.3.0
zend_optimizer.version=3.3.0a
```

And here is the final result with no more SEGFAULTS

```shell
php -v
PHP 4.4.7 (cli) (built: May 4 2007 11:42:28)
Copyright (c) 1997-2007 The PHP Group
Zend Engine v1.3.0, Copyright (c) 1998-2004 Zend Technologies
with XCache v1.2.1, Copyright (c) 2005-2007, by mOo
with the ionCube PHP Loader v3.1.22, Copyright (c) 2002-2006, by ionCube Ltd., and
with Zend Extension Manager v1.2.2, Copyright (c) 2003-2007, by Zend Technologies
with Zend Optimizer v3.3.0, Copyright (c) 1998-2007, by Zend Technologies
```
