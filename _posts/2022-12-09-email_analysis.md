---
title: "Email Analysis"
categories: 
  - informationsecurity
tags: 
  - email analysis
  - blue team
classes: 
  - wide
excerpt: ""
toc: true
date: 2022-12-09
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
* [IPinfo.io](https://steh.github.io)
  * A service that provides detailed information about an IP address by focusing on geolocation data and service provider.
* [Talos Reputation](https://steh.github.io)
  * An IP reputation check service is provided by Cisco Talos.
* [Urlscan.io](https://steh.github.io)
  * A service that analyses websites by simulating regular user behaviour.
* [Browserling](https://steh.github.io)
  * A browser sandbox is used to test suspicious/malicious links.
* [Wannabrowser](https://steh.github.io)
  * A browser sandbox is used to test suspicious/malicious links.
* <https://emailrep.io/>

## Refrences

* [TryHackme Advent of Cyber Day 6](https://tryhackme.com/room/adventofcyber4)
