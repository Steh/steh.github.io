---
title:  "The Cyber Kill Chain"
date:   2022-11-18
categories: informationsecurity frameworks
---

1. Recon - Reconnaissance
    *  is where the attacker tries to learn as much as possible about the target
    *  such as the types of servers, operating system, IP addresses, names of users, and email addresses, can help the attack’s success.
    *  OSINT falls under this step [^1]
    *  Tools for this steep:
        * [theHarvester](https://github.com/laramies/theHarvester) - commandline tool to get data from multiple public data sources
        * [Hunter.io](https://hunter.io/try/search/) - email hunting tool 
        * [OSINT Framework](https://osintframework.com/) - collection of OSINT tools
2. Weaponization
    * preparing a file with a malicious component
3. Delivery
    * delivering the “weaponized” file to the target
    * examples: Phishing or infected USB-Devices [^2]
4. Exploitation
   * execute the malicious component
5. Installation: 
   * install the malware on the target system
   * including backdoor to gain persistance [^3]
6. Command & Control (C2)
   * the attacker has the ability to command and control the target system.
   * most common communication channels: HTTP/s and DNS Tunneling
7. Actions on Objectives
   * achieve their objectives, like Data Exfiltration

The Cyber Kill Chain was created and last updated in 2011. More modern approaches are [MITRE ATT&CK](https://attack.mitre.org/) and [Unified Kill Chain](https://unifiedkillchain.com/).

# References
- https://tryhackme.com/room/intronetworksecurity
- https://www.lockheedmartin.com/en-us/capabilities/cyber/cyber-kill-chain.html
- https://www.trustedsec.com/blog/intro-to-macros-and-vba-for-script-kiddies/

[^1]: https://www.varonis.com/blog/what-is-osint
[^2]: https://www.csoonline.com/article/3534693/cybercriminal-group-mails-malicious-usb-dongles-to-targeted-companies.html
[^3]: https://www.offensive-security.com/metasploit-unleashed/meterpreter-backdoor/
