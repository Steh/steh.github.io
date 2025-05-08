---
title: "The Cyber Kill Chain"
categories: 
  - informationsecurity
tags: 
  - frameworks
classes: 
  - wide
excerpt: ""
toc: true
date: 2022-11-26
---

## The Cyber Kill Chain

1. Recon - Reconnaissance
    * The attacker tries to learn as much as possible about the target, such as the types of servers, operating system, IP addresses, names of users, and email addresses, which can help the success of the attack.
    * OSINT falls under this step [^1]
    * Tools for this step:
        * [theHarvester](https://github.com/laramies/theHarvester) - Command-line tool to get data from multiple public data sources
        * [Hunter.io](https://hunter.io/try/search/) - Email hunting tool
        * [OSINT Framework](https://osintframework.com/) - Collection of OSINT tools
2. Weaponization
    * Preparing a file with a malicious component
3. Delivery
    * Delivering the "weaponized" file to the target
    * Examples: Phishing or infected USB devices [^2]
4. Exploitation
    * Execute the malicious component
5. Installation:
    * Install the malware on the target system, including backdoor to gain persistence [^3]
6. Command & Control (C2)
    * The attacker has the ability to command and control the target system.
    * Most common communication channels: HTTP/s and DNS Tunneling
7. Actions on Objectives
    * Achieve their objectives, such as data exfiltration

The Cyber Kill Chain was created and last updated in 2011. For a better view, it can be combined with more modern approaches like [MITRE ATT&CK](https://attack.mitre.org/) and [Unified Kill Chain](https://unifiedkillchain.com/).

## References

* [TryHackMe: Network Security](https://tryhackme.com/room/intronetworksecurity)
* [Lockheed Martin: Cyber Kill Chain](https://www.lockheedmartin.com/en-us/capabilities/cyber/cyber-kill-chain.html)
* [Intro to Macros and VBA for Script Kiddies](https://www.trustedsec.com/blog/intro-to-macros-and-vba-for-script-kiddies/)

[^1]: [https://www.varonis.com/blog/what-is-osint](https://www.varonis.com/blog/what-is-osint)
[^2]: [https://www.csoonline.com/article/3534693/cybercriminal-group-mails-malicious-usb-dongles-to-targeted-companies.html](https://www.csoonline.com/article/3534693/cybercriminal-group-mails-malicious-usb-dongles-to-targeted-companies.html)
[^3]: [https://www.offensive-security.com/metasploit-unleashed/meterpreter-backdoor/](https://www.offensive-security.com/metasploit-unleashed/meterpreter-backdoor/)
