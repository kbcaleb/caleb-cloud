---
title: Make a FreeBSD 7.0 DVD
date: 2008-05-08 11:17:06.000000000 -06:00
categories:
  - freebsd
tags:
  - freebsd
---
The goal here is to make 1 single DVD out of the 3 FreeBSD 7.0  installation CD’s. First we need to fetch all 3 of the ISO’s. For this  example I am pulling the i386 version.
```shell
wget ftp://ftp.freebsd.org/pub/FreeBSD/releases/i386/ISO-IMAGES/7.0/7.0-RELEASE-i386-disc1.iso
wget ftp://ftp.freebsd.org/pub/FreeBSD/releases/i386/ISO-IMAGES/7.0/7.0-RELEASE-i386-disc2.iso
wget ftp://ftp.freebsd.org/pub/FreeBSD/releases/i386/ISO-IMAGES/7.0/7.0-RELEASE-i386-disc3.iso
```
Now lets mount them each as a loopback and then get the contents.
```shell
mount -t iso9660 -o loop /path/to/7.0-RELEASE-i386-disc3.iso /mnt
mkdir ~/FreeBSD-DVD-7.0 &amp;&amp; cd ~/FreeBSD-DVD-7.0
tar -C /mnt -cf - . |tar -xf -
umount /mnt
mount -t iso9660 -o loop /path/to/7.0-RELEASE-i386-disc2.iso /mnt
tar -C /mnt -cf - . |tar -xf -
umount /mnt
mount -t iso9660 -o loop /path/to/7.0-RELEASE-i386-disc1.iso /mnt
tar -C /mnt -cf - . |tar -xf -
umount /mnt
cat cdrom.inf
CD_VERSION = 6.1-RC1
CD_VOLUME = 1
cd packages
cat INDEX | sed -e "s/|2/|1/g" -e "s/|3/|1/g" &gt; NEWINDEX
mv NEWINDEX INDEX
growisofs -Z /dev/cd0 -speed 16 -J -R -no-emul-boot -b boot/cdboot -iso-level 3 temp
```
The last bit here on the INDEX file is to remove reference to CD’s 2&amp;3 so it will use the 1 DVD for all packages.
