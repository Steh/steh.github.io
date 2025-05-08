---
title: "smtp-user-enum"
date: 2022-07-11
categories:
- Information Security
tags:
- smtp-user-enum
- Kali
classes: 
- wide
---

```bash
smtp-user-enum -M VRFY -U users.txt -t 10.10.10.1
smtp-user-enum -M VRFY -u tom -t 10.10.10.1
```

## References

* [kali-smtp-user-enum](https://www.kali.org/tools/smtp-user-enum/)
