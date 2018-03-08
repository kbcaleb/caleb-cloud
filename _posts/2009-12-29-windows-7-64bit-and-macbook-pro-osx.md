---
title: Windows 7 64bit and Macbook Pro (osX)
date: 2009-12-29 11:29:48.000000000 -07:00
categories:
  - mac
  - windows
tags:
  - mac
  - windows
---
So the first hurdle I had to overcome was a bad bootable disc that  was given to us from Microsoft. Whenever I used the CD they gave us in  my macbook I would get the following on boot.
```shell
    1.
    2.
Select CD-ROM Boot Type :

```
Now this error is not supposed to create issues with newer unibody  macbook pros because they have the newer BIOS compatibility layer. This  problem occurs because the ETFSBOOT.COM program does not handle file  versions according to the International Standards Organization (ISO)  9660 specification. The ISO 9660 specification instructs that a name for  a file record should consist of the file name that is followed by the  file version. Also, the specification instructs that you must separate  the file name and the file version by a semicolon. For example, the  following file record is valid:
```shell
filename;1
```
The Windows PE file system driver handles the file version as an  option. However, the ETFSBOOT.COM program cannot locate the  Setupldr.bin/Bootmgr file if you use a file version. Therefore, if you  use a program other than CDimage.exe or OSCDimg.exe to create the CDFS  image file, or another program that will not allow you to remove the ;1  versioning, then you will not be able to boot from the CD.
So now lets fix the boot section by rebuilding to ISO correctly.  First of all I will be doing this in Linux with Wine but you can do it  Windows as well by changing the paths up some.<br />
First lets install wine and set it up.
```shell
apt-get install wine
winecfg

```
Now lets get the required exe file
```shell
cd ~/.wine/drive_c
wget http://ccollins.net/files/oscdimg.exe

```
Now lets create the required directories.
```shell
mkdir ~/.wine/drive_c/win7iso &amp;&amp; mkdir ~/.wine/drive_c/win7dvd

```
Now lets mount the ISO and copy all the files in to the new win7iso directory.
```shell
mount -o loop en_windows_7_enterprise_x64_dvd_x15-70749.iso /mnt
cp -R /mnt/* ~/.wine/drive_c/win7iso/

```
Now lets build the new ISO
```shell
cd ~/.wine/drive_c
wine oscdimg.exe -n -m -bc:win7iso/boot/etfsboot.com c:win7iso c:win7dvd/win7_64_ent.iso

```
Now mount the ISO and verify all the files are there
```shell
mount -o loop ~/.wine/drive_c/win7dvd/win7_64_ent.iso /mnt

```
If they are all there simply unmount /mnt and burn the new ISO you  have. When you boot the first time into windows you will need to setup  BootCamp. The first thing you should do is the following.<br />
Start Menu -&gt; Programs -&gt; Accessories -&gt; Command Prompt (Right Click &amp; choose “Run as Administrator”)<br />
Now start the BootCamp64.msi manually like this.
```shell
d:
cd Boot Camp\Drivers\Apple
BootCamp64.msi

```
This will bypass the check the the normal setup.exe does and allow  you to install everything required. If you want to edit the setup.exe  file and remove the depend lines.
