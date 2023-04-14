---
title:  "smtp-user-enum"
date:   2022-07-11
categories: 
- informationsecurity
tags:
- smtp-user-enum
- kali
---

{% highlight bash %}
smtp-user-enum -M VRFY -U users.txt -t 10.10.10.1
smtp-user-enum -M VRFY -u tom -t 10.10.10.1
{% endhighlight %}

## References

* [kali-smtp-user-enum](https://www.kali.org/tools/smtp-user-enum/)
