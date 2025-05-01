---
title:  "Wireshark"
date:   2022-12-16
excerpt: "A guide to analyzing network traffic with Wireshark, including checklists, filters, and tips."
categories: informationsecurity
tags: 
  - Wireshark
  - blue team
toc: true
toc_label: "Table of Contents"
toc_icon: "cog"
classes: wide
---

## Checklist for Analyzing

### Checks to Perform
- Packet statistics
- Service identification
- IP reputation check

### Questions to Answer

- Which IP addresses are in use?
- Has a suspicious IP address been detected?
- Has suspicious port usage been detected?
- Which port numbers and services are in use?
- Is there an abnormal level of traffic on any port or service?

## How to Analyze Captured Traffic

### Preparation and Research

- View the overall usage of ports and services:
  - *"Statistics --> Protocol Hierarchy"*
- View the list of IP conversations to find:
  - *"Statistics --> Conversations"*
- On the TCP/UDP tab from *Conversations*, you can see the ports used.
- Gather the following information:
  - Source and destination IP addresses
  - Protocols
  - Port numbers
  - Services

### Starting to Filter

- Start by looking at DNS traffic:
  ```
dns
```

- Export transmitted files:
  - *File -> Export Objects -> HTTP*

### Checks to Perform
- Shared files
- File hashes (SHA256)
- Hash reputation check

### Questions to Answer
- What are the shared files?
- Does the hash reputation mark them as suspicious or malicious?
- Which domain hosts the suspicious/malicious file?

## Enabling TLS Decryption

- Navigate to: *Edit > Preferences > Protocols > SSL (or TLS if present) > (Pre)-Master-Secret log filename.*

## Filter Examples

```bash
# Filter by IP/MAC
ip.addr == x.x.x.x 
ip.src == x.x.x.x
ip.dest == x.x.x.x && ip.src == x.x.x.x

# Filter by MAC
eth.addr == x.x.x.x

# Filter by port
dst port 135 and tcp port 135

# Find HTTP packages with data
http && (media || data-text-lines)
```

## References

- [Wireshark Filter Manual Page][def1]
- [Wireshark Cheat Sheet on GitHub][def3]
- [Wireshark Filter Reference][def4]
- [OWASP Wireshark Presentation][def2]
- [TryHackMe: Advent of Cyber Day 13][def5]

[def1]: https://www.wireshark.org/docs/man-pages/wireshark-filter.html
[def2]: https://owasp.org/www-pdf-archive//Owasp_wireshark.pdf
[def3]: https://github.com/security-cheatsheet/wireshark-cheatsheet
[def4]: https://www.wireshark.org/docs/dfref/
[def5]: https://tryhackme.com/room/adventofcyber4
