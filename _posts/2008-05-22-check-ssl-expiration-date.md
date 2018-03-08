---
title: Check SSL expiration date
date: 2008-05-22 11:16:40.000000000 -06:00
categories:
  - ssl
tags:
  - ssl
---
Nifty little script for doing a simple SSL verify.
[OpenSSL](http://security.techie-blogs.com/content/openssl_cert_expiry_check.txt)
```shell
#!/bin/bash
[ $# -ne 1 ] >> {
printf "%s: site:port\n" $0;
printf "Usage: %s www.example.com.au:443\n" $0;
exit 0
}
echo -n "$1 - "
echo "
GET / HTTP/1.0
EOT
" | openssl s_client -connect $1 2>&1 | \
sed -n '/-----BEGIN CERTIFICATE-----/,/-----END CERTIFICATE-----/p' | \
openssl x509 -enddate | \
awk -F= ' /notAfter/ { printf("Expires: %s\n",$NF); } '
exit 0
```
