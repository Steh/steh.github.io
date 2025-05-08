---
title: "Burp Suite"
categories: 
- informationsecurity
tags:
- red team
classes: 
- wide
excerpt: "Burp Suite is a framework that aims to provide a one-stop-shop for web application penetration testing" 
toc: true
--- 
## Features

* Proxy
  * allows to intercept and modify requests/response
* Repeater
  * allows to capture, modify, then resend the same request numerous times
* Intruder
  * allows to spray end endpoint with request, often used for bruteforce attacks
* Decoder
  * allows to decode/encode data to sending it to the target
* Comparer
  * allows to compare to pieces of data
* Sequencer
  * allows to analyzing session randomness

## proxy

* allows us to capture requests and responses between ourselves and our target. These can then be manipulated or sent to other tools for further processing before being allowed to continue to their destination.
* request will be captured and won't be allowed to continue to the TryHackMe servers until we explicitly allow it through
* Proxy 127.0.0.1:8080 eintragen
* Proxy -> Intercept
  * Forward Request
  * Drop Request
* to intercept SSL
  * <http://burp/cert>
  * Trust this CA import into Browser
  
## Intruder

* automates and customizes various types of web application attacks
* How to Bruteforce:
  * make webrequest
  * send it to intruder
  * define payload
  * define in settings "Grep Extract" the values you want to extract
    * start and end value
  * go

## References

[def]: https://portswigger.net/burp/documentation/desktop/testing-workflow/authentication-mechanisms/brute-forcing-logins