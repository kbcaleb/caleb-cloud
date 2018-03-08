---
title: Postfix+Amavisd+ClamAV+SpamAssassin+Razor+SMTP Auth
date: 2009-12-21 11:28:30.000000000 -07:00
categories:
  - mail
tags:
  - mail
header:
  teaser: "/assets/images/spam.png"
  show_overlay_excerpt: false
---
First lets install the require software
```shell
yum install clamd amavisd-new spamassassin razor-agents cyrus-sasl-md5
```
Now lets add some entries to the /etc/postfix/main.cf file
```shell
header_checks = regexp:/usr/local/etc/postfix/header_checks
smtpd_sasl_auth_enable = yes
smtpd_sasl_security_options = noanonymous
broken_sasl_auth_clients = yes
smtpd_client_restrictions =
   check_client_access hash:/usr/local/etc/postfix/blackwhite.map,
   reject_non_fqdn_hostname,
   reject_non_fqdn_sender,
   reject_unknown_sender_domain,
   permit_mynetworks,
   reject_rbl_client sbl.spamhaus.org,
   reject_rbl_client bl.spamcop.net,
   permit

smtpd_sender_restrictions =
   check_sender_access hash:/usr/local/etc/postfix/blackwhite.map,
   reject_unknown_sender_domain,
   reject_non_fqdn_sender,
   permit

smtpd_recipient_restrictions =
   permit_sasl_authenticated,
   check_recipient_access hash:/usr/local/etc/postfix/blackwhite.map,
   reject_non_fqdn_hostname,
   reject_non_fqdn_sender,
   reject_non_fqdn_recipient,
   reject_unknown_sender_domain,
   permit_mynetworks,
   reject_unauth_destination,
   permit

### Tarpit those bots/clients/spammers who send errors or scan for accounts
smtpd_error_sleep_time = 60
smtpd_soft_error_limit = 60
smtpd_hard_error_limit = 10
```
Now lets create our blackwhite.map files
```shell
touch /etc/postfix/blackwhite.map
```
Add your entries like this
```shell
user@domain.com OK
user@spamdomain.com REJECT
```
Reload your black &amp; white maps
```shell
postmap /etc/postfix/blackwhite.map
postfix reload
```
Now edit you /etc/postfix/master.cf file and change the smtp entry to be like this.
```shell
smtp inet n - n - - smtpd
# -o content_filter=smtp-amavis:[127.0.0.1]:10024
```
If you want to use pre-queue filtering then use the following entry.
```shell
smtp inet n - n - - smtpd
# -o smtpd_proxy_filter=smtp-amavis:[127.0.0.1]:10024
```
Now we need to edit the /etc/postfix/master.cf by adding this to the bottom to allow mail from Amavis to come back in.
```shell
smtp-amavis unix -      -       -     -       2  smtp
    -o smtp_data_done_timeout=1200
    -o disable_dns_lookups=yes
127.0.0.1:10025 inet n  -       -     -       -  smtpd
    -o content_filter=
    -o local_recipient_maps=
    -o relay_recipient_maps=
    -o smtpd_restriction_classes=
    -o smtpd_client_restrictions=
    -o smtpd_helo_restrictions=
    -o smtpd_sender_restrictions=
    -o smtpd_recipient_restrictions=permit_mynetworks,reject
    -o mynetworks=127.0.0.0/8
    -o strict_rfc821_envelopes=yes
```
Add the following to /etc/alias to create a virus alert alias.
```shell
virusalert: root
```
Now reload the new alias file.
```shell
postalias /etc/aliases
```
Now restart postfix and verify you have port 10025 open.
```shell
netstat -ntpl | grep 25
```
You should see the following.
```shell
tcp 0 0 0.0.0.0:225 0.0.0.0:* LISTEN 2896/sbadm
tcp 0 0 127.0.0.1:10025 0.0.0.0:* LISTEN 30724/master
tcp 0 0 0.0.0.0:25 0.0.0.0:* LISTEN 30724/master
```
Now lets setup Amavis by editing /etc/amavisd.conf. Set your desired  Anti-Virus and your hostname and any other options you would like.
```shell
$mydomain = 'example.com'; # a convenient default for other settings
$final_virus_destiny = D_DISCARD;
$final_banned_destiny = D_BOUNCE;
$final_spam_destiny = D_PASS;
@av_scanners = (

# ### http://www.clamav.net/
['ClamAV-clamd',
<pre wp-pre-tag-12>amp;ask_daemon, ["CONTSCAN {}\n", "/var/amavis/clamd"],
qr/\bOK$/m, qr/\bFOUND$/m,
qr/^.*?: (?!Infected Archive)(.*) FOUND$/m ],
```
Now lets create a few required directories.
```shell
mkdir -p /var/amavis/{clamav,.spamassassin,.razor}
chown -R amavis:amavis /var/amavis/
chgrp -R amavis /var/log/clamav
chmod 775 /var/log/clamav
chmod -R 664 /var/log/clamav/*
chgrp -R amavis /var/clamav
chmod 664 /var/clamav/mirrors.dat
```
We need to setup logrotate to keep these permissions by editing the “create” line in the following files.<br />
/etc/logrotate.d/clamav<br />
/etc/logrotate.d/freshclam
```shell
create 664 clamav amavis
```
Now lets edit /etc/clamd.conf
```shell
User amavis
LocalSocket /var/amavis/clamd
```
Now lets modify the /etc/freshclam.conf
```shell
DatabaseOwner amavis
```
Now lets start setting up Razor
```shell
su - amavis
razor-admin -create
razor-admin -discover
razor-admin -register -user postmaster@yourdomain.com
exit
```
This should store the file in a location like this so you can view it for your user and password.
```shell
cat /var/amavis/.razor/identity-postmaster@yourdomain.com
pass = blahblahblahmehmehmehblah
user = postmaster@yourdomain.com
```
Next lets edit /etc/mail/spamassassin/local.cf. These setting are  just what I used and you would be best setting your own custom setting  most likely.
```shell
skip_rbl_checks 1
use_bayes 1
bayes_path /var/amavis/.spamassassin/bayes
use_razor2 1
use_pyzor 0
dns_available yes
header LOCAL_RCVD Received =~ /\S+\.section6.net\s+\(.*\[.*\]\)/
score LOCAL_RCVD -50
score DCC_CHECK 4.000
score RAZOR2_CHECK 2.500
score BAYES_99 5.300
score BAYES_90 4.500
score BAYES_80 4.000
score HTML_FONT_INVISIBLE 3
score HTML_FONTCOLOR_UNKNOWN 2
score ORDER_NOW 1.5
score CLICK_BELOW 1
score LIMITED_TIME_ONLY 1
score HTML_IMAGE_ONLY_02 2
score HTML_IMAGE_ONLY_04 2
score OFFERS_ETC 2
score HTML_LINK_CLICK_HERE 1
score LINES_OF_YELLING 1
```
Now we can start amavis and set it to start on reboots always.
```shell
/etc/rc.d/init.d/amavisd start
chkconfig amavisd on
```
Now we can start clamd
```shell
/etc/rc.d/init.d/clamd start
chkconfig clamd on
```
Now uncomment the following line that you added to the /etc/postfix/master.cf file.
```shell
# -o content_filter=smtp-amavis:[127.0.0.1]:10024
```
Now reload postfix
```shell
postfix reload
```
Now we can verify if SMTP Auth is working.
```shell
telnet 0 25
```
Now type EHLO yourdomain.com and you should get the following showing you MD5 support fot login.
```shell
250-br0ck.bigkernel.com
250-PIPELINING
250-SIZE 10240000
250-VRFY
250-ETRN
250-STARTTLS
250-AUTH PLAIN LOGIN CRAM-MD5 DIGEST-MD5
250-AUTH=PLAIN LOGIN CRAM-MD5 DIGEST-MD5
250-ENHANCEDSTATUSCODES
250-8BITMIME
250 DSN
```
From here you should be all set so that incoming messages hit Postfix  and then gets shoved off to Amavis where the Spam and Virus scanning  will take place and then it will be delivered back to Postfix on port  10025.
