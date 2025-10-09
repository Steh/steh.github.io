---
title: ""
categories: 
- informationsecurity
tags:
- blue team
classes: 
- wide
excerpt: "" 
toc: true
--- 

## hydra
hydra -l <user> -P /usr/share/wordlists/rockyou.txt <ip> -s <port> http-get -m <path>

## Anti-CSRF Tokens

> Anti-CSRF tokens are random values sent inside web application forms (such as login forms) that are tracked by the application. If a form is submitted without a valid CSRF token, the application will reject the submission.



## source

* [Immersive Labs: Authentication and Authorization Flaws][def]

[def]: https://immersivelabs.online/series/authentication-and-authorisation-flaws/labs?category=web-app-hacking
