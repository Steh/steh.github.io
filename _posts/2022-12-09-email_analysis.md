---
title:  "email analysis"
date:   2022-12-09
excerpt: ""
categories: informationsecurity
tags: 
- email analysis
- blue team
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
classes: wide
---

## emlAnalyzer

```bash
# Extract Informations
emlAnalyzer -i mail.eml --header --html -u --text --extract-all

# Attachments will be saved to:
eml_attachments
```

## OSINT Tools for analysing

* [VirusTotal](https://www.virustotal.com/gui/home/search)
  * A service that provides a cloud-based detection toolset and sandbox environment.
* [InQuest](https://labs.inquest.net/)
  * A service provides network and file analysis by using threat analytics.
* [IPinfo.io]()
  * A service that provides detailed information about an IP address by focusing on geolocation data and service provider.
* [Talos Reputation]()
  * An IP reputation check service is provided by Cisco Talos.
* [Urlscan.io]()
  * A service that analyses websites by simulating regular user behaviour.
* [Browserling]()
  * A browser sandbox is used to test suspicious/malicious links.
* [Wannabrowser]()
  * A browser sandbox is used to test suspicious/malicious links.
* <https://emailrep.io/>

## Refrences

* [TryHackme Advent of Cyber Day 6](https://tryhackme.com/room/adventofcyber4)
