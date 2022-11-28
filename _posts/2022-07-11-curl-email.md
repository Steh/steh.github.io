---
title:  "fun with curl"
date:   2022-07-11
categories: 
- informationsecurity
tags:
- curl
---

# E-Mail
Send an Mail through curl
```bash
# mail template
From: from@steh.de
To:   to@steh.de
Subject: curl E-Mail

Hey,

dies ist eine Mail die mit curl verschickt wurde.

# send mail
curl  -vk smtp://mailserver.de --mail-from from@steh.de --mail-rcpt  to@steh.de  --ssl --upload-file mail.txt
```

* [everything-curl](https://everything.curl.dev/usingcurl/smtp)
* [stackoverflow-using-curl-to-send-email](https://stackoverflow.com/questions/14722556/using-curl-to-send-email)
* [linuxshelltips_curl-send-email-linux](https://www.linuxshelltips.com/curl-send-email-linux/)

# logon
Send Post Request to a Logon Page.
```bash
# find values for request
curl http://XX.XX.XX.XX/admin.php

# send data
curl -X POST -d "username=admin" -d "password=admin" http://XX.XX.XX.XX/admin.php
```