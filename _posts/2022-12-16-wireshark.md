---
title:  "Wireshark"
date:   2022-12-16
excerpt: ""
categories: informationsecurity
tags: 
- Wireshark
- blue team
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
classes: wide
---
## Checklist for Analysing

* Checks to do
  * Packet statistics
  * Service identification
  * IP reputation check
* Questions to answer
  * Which IP addresses are in use?
  * Has a suspicious IP address been detected?
  * Has suspicious port usage been detected?
  * Which port numbers and services are in use?
  * Is there an abnormal level of traffic on any port or service?
Reference[^1]

## How Analyse Captured Traffic

### Preparation and Research

* View the overall usage of the ports and services
  * *"Statistics --> Protocol Hierarchy"*
* View the list of IP conversations, to find
  * *"Statistics --> Conversations"*
* On the TCP/UDP Tap from *Conversations* you can see the Ports used
* Now you have the following informations
  * Source and destination IP addresses
  * Protocols
  * Port numbers
  * Services

### Starting to Filter

* Looking at the DNS Traffic is always a good way to start
  * ```dns```

* Export Transmitted Files
  * File -> Export Objects -> HTTP

* **Checks to do**
  * Shared files
  * File hashes (SHA256)
  * Hash reputation check
* **Questions to answer**
  * What are shared files?
  * Does the hash reputation marked as suspicious or malicious?
  * Which domain hosts the suspicious/malicious file?  

## enable TLS decryption

* Edit > Preferences > Protocols > SSL (or TLS if present) > (Pre)-Master-Secret log filename.

## filter examples

```bash
## Filter by IP/MAC
ip.addr == x.x.x.x 
ip.src == x.x.x.x
ip.dest == x.x.x.x && ip.src == x.x.x.x

## Filter by mac
eth.addr == x.x.x.x

## filter by port
dst port 135 and tcp port 135
```

* [wireshark-filter(4) Manual Page][def1]
* [https://github.com/security-cheatsheet/wireshark-cheatsheet][def3]
* [Wireshark filter reference][def4]

## References

* [OWASP Wireshark presentation][def2]
* [tryhackme: Advent of Cyber Day 13]([https://tryhackme.com/room/adventofcyber4](https://tryhackme.com/room/adventofcyber4))

[def1]: https://www.wireshark.org/docs/man-pages/wireshark-filter.html
[def2]: https://owasp.org/www-pdf-archive//Owasp_wireshark.pdf
[def3]: https://github.com/security-cheatsheet/wireshark-cheatsheet
[def4]: https://www.wireshark.org/docs/dfref/
