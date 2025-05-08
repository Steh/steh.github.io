---
title: "Generate User/Password Lists with Crunch"
date: 2022-07-11
categories:
- Information Security
tags:
- Crunch
- Kali
- Linux
- Wordlist
- Password
classes:
- wide
---

Generate password or user lists on Linux with Crunch.

```bash
# Create wordlists
## 1 5          = Character count between 1 and 5
## rstuvwxyz    = All included characters
## -o           = Output file
crunch 1 5 rstuvwxyz -o /root/users.txt

## Basic command
crunch <min. password length> <max. password length> <character space> -o <saving_location>

## References

* [Kali: crunch](https://www.kali.org/tools/crunch/)
