---
layout: post
title:  "curl: E-Mails verschicken"
date:   2022-07-11
categories: curl
---

{% highlight bash %}
From: from@steh.de
To:   to@steh.de
Subject: curl E-Mail

Hey,

dies ist eine Mail die mit curl verschickt wurde.

{% endhighlight %}

{% highlight bash %}
curl  -vk smtp://mailserver.de --mail-from from@steh.de --mail-rcpt  to@steh.de  --ssl --upload-file mail.txt
{% endhighlight %}

[everything-curl]: https://everything.curl.dev/usingcurl/smtp
[stackoverflow-using-curl-to-send-email]: https://stackoverflow.com/questions/14722556/using-curl-to-send-email
[linuxshelltips_curl-send-email-linux]: https://www.linuxshelltips.com/curl-send-email-linux/
