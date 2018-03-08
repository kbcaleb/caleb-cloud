---
title: Log vsftpd to MySQL
date: 2008-02-13 11:18:43.000000000 -07:00
categories:
  - vsftpd
  - mysql
tags:
  - vsftpd
  - mysql
header:
  teaser: "/assets/images/mysql.png"
  show_overlay_excerpt: false
---
First lets build the pam_mysql package. There is more then one way to do this I just decided to use a SRC RPM I found for FC9.
```shell
wget http://rpm.pbone.net/index.php3/stat/3/srodzaj/2/search/pam_mysql-0.7-0.1.rc1.fc9.src.rpm
rpm -ivh pam_mysql-0.7-0.1.rc1.fc9.src.rpm
rpmbuild -bb /usr/src/redhat/SPECS/pam_mysql.spec
rpm -ivh /usr/src/redhat/RPMS/i386/pam*.rpm
```
Now that we have the pam module installed lets enable it for VsFTPd by creating the required user and conf file
```shell
useradd -d /home/vsftpd -g nobody -m -s /bin/false vsftpd
cp /etc/vsftpd/vsftpd.conf /etc/vsftpd/vsftpd.conf.orig
```
Now I just use the following in my vsftpd.conf file you can add more but this is the minimum you will need to make it work.
```shell
listen=YES
anonymous_enable=NO
local_enable=YES
write_enable=YES
local_umask=022
dirmessage_enable=YES
xferlog_enable=YES
connect_from_port_20=YES
nopriv_user=vsftpd
chroot_local_user=YES
secure_chroot_dir=/var/run/vsftpd
pam_service_name=vsftpd
guest_enable=YES
guest_username=vsftpd
local_root=/home/vsftpd/$USER
user_sub_token=$USER
virtual_use_local_privs=YES
```
Now lets correct pam authentication
```shell
cp /etc/pam.d/vsftpd /etc/pam.d/vsftpd.orig
```
Now you simply add the following to your /etc/pam.d/vsftpd file(you  only need these entries in the file). Please note that these lines  include logging support to MySQL, so if you don’t want this then please  just remove the last part from sqllog=1 to the last part of verbose=1.
```shell
auth required pam_mysql.so user=vsftpd passwd=rackspace host=localhost db=vsftpd table=accounts usercolumn=username passwdcolumn=pass crypt=0 sqllog=1 logtable=logs logmsgcolumn=msg logusercolumn=user logpidcolumn=pid loghostcolumn=host logtimecolumn=logtime verbose=1
account required pam_mysql.so user=vsftpd passwd=rackspace host=localhost db=vsftpd table=accounts usercolumn=username passwdcolumn=pass crypt=0 sqllog=1 logtable=logs logmsgcolumn=msg logusercolumn=user logpidcolumn=pid loghostcolumn=host logtimecolumn=logtime verbose=1
```
I used crypt=0 in this example because I had issues getting the MD5  portion to work with pam_mysql. You could of course change this but it  will only effect how the password field is read from MySQL.<br />
Now lets create a testuser
```shell
>mkdir /home/vsftpd/testuser
chown vsftpd:nobody /home/vsftpd/testuser
```
Now lets setup the DB and the user.
```sql
CREATE DATABASE vsftpd;
GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP ON vsftpd.* TO 'vsftpd'@'localhost' IDENTIFIED BY 'password';
flush privileges;
```
Now lets create the required tables.
```sql
use vsftpd;
CREATE TABLE accounts (
id INT NOT NULL AUTO_INCREMENT PRIMARY KEY ,
username VARCHAR( 30 ) NOT NULL ,
pass VARCHAR( 50 ) NOT NULL ,
UNIQUE (username)
) ENGINE = MYISAM ;
create table logs (msg varchar(255),
user char(16),
pid int,
host char(32),
rhost char(32),
logtime timestamp
);
quit;
```
Now we can add the testuser
```sql
use vsftpd;
INSERT INTO accounts (username, pass) VALUES('testuser', 'secret');
```
Now if you got MD5 to work correctly when building the RPM then you could use the following instead
```sql
use vsftpd;
INSERT INTO accounts (username, pass) VALUES('testuser', PASSWORD('secret'));
```
Now restart vsftpd and login
