---
layout: post
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
3. Weaponization
    * preparing a file with a malicious component
5. Delivery: Delivery means delivering the “weaponized” file to the target via any feasible method, such as email or USB flash memory.
6. Exploitation: When the user opens the malicious file, their system executes the malicious component.
7. Installation: The previous step should install the malware on the target system.
8. Command & Control (C2): The successful installation of the malware provides the attacker with a command and control ability over the target system.
9. Actions on Objectives: After gaining control over one target system, the attacker has achieved their objectives. One example objective is Data Exfiltration (stealing target’s data).

* https://tryhackme.com/room/intronetworksecurity
* https://www.lockheedmartin.com/en-us/capabilities/cyber/cyber-kill-chain.html

[^1]: https://www.varonis.com/blog/what-is-osint
