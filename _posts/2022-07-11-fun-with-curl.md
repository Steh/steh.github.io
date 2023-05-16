---
title: "Fun with Curl"
date: 2022-07-11
categories:
- Information Security
tags:
- Curl
classes:
- wide
toc: true
excerpt: "An overview of what you can do with curl."
---

## E-Mail

Send an email through curl:

```bash
# Mail template
From: from@steh.de
To: to@steh.de
Subject: curl E-Mail

Hey,

this is an email sent using curl.

# Send mail
curl -vk smtp://mailserver.de --mail-from from@steh.de --mail-rcpt to@steh.de --ssl --upload-file mail.txt
```

## Logon

Send a POST Request to a logon page.

```bash
# Find values for request
curl http://XX.XX.XX.XX/admin.php

# Send data
curl -X POST -d "username=admin" -d "password=admin" http://XX.XX.XX.XX/admin.php
```

## Reference

* [everything-curl](https://everything.curl.dev/usingcurl/smtp)
* [stackoverflow-using-curl-to-send-email](https://stackoverflow.com/questions/14722556/using-curl-to-send-email)
* [linuxshelltips_curl-send-email-linux](https://www.linuxshelltips.com/curl-send-email-linux/)
