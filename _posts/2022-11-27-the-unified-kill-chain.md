---
title:  "The Unified Kill Chain"
date:   2022-11-27
excerpt: "A quick overview of The Unified Kill Chain Model"
categories: informationsecurity
tags: [frameworks, ukc, security, informationsecurity]
layout: single
---

1. TOC
{:toc}

# Overview of the attack phases [^1]

|  Attack |  Phase | Description |
|  ----------- |  ----------- | ----------- |
| 1 | Reconnaissance| Researching, identifying and selecting targets using active or passive reconnaissance.|
| 2 | Weaponization| Preparatory activities aimed at setting up the infrastructure required for the attack.|
| 3 | Delivery| Techniques resulting in the transmission of a weaponized object to the targeted environment.|
| 4 | Social Engineering| Techniques aimed at the manipulation of people to perform unsafe actions.|
| 5 | Exploitation| Techniques to exploit vulnerabilities in systems that may, amongst others, result in code execution.|
| 6 | Persistence| Any access, action or change to a system that gives an attacker persistent presence on the system.|
| 7 | Defense Evasion| Techniques an attacker may specifically use for evading detection or avoiding other defenses.|
| 8 | Command & Control| Techniques that allow attackers to communicate with controlled systems within a target network.|
| 9 | Pivoting |Tunneling traffic through a controlled system to other systems that are not directly accessible.|
| 10  | Discovery |Techniques that allow an attacker to gain knowledge about a system and its network environment.|
| 11  | Privilege Escalation| The result of techniques that provide an attacker with higher permissions on a system or network.|
| 12  | Execution| Techniques that result in execution of attacker-controlled code on a local or remote system.|
| 13  | Credential Access| Techniques resulting in the access of, or control over, system, service or domain credentials.|
| 14  | Lateral Movement| Techniques that enable an adversary to horizontally access and control other remote systems.|
| 15  | Collection |Techniques used to identify and gather data from a target network prior to exfiltration.|
| 16  | Exfiltration |Techniques that result or aid in an attacker removing data from a target network.|
| 17  | Impact| Techniques aimed at manipulating, interrupting or destroying the target system or data.|
| 18  | Objectives| Socio-technical objectives of an attack that are intended to achieve a strategic goal.|

## in
![Cyber Kill Chain In]({{ site.url }}/assets/images/cyber-kill-chain-in.png) [^1]
## throug
![Cyber Kill Chain through]({{ site.url }}/assets/images/cyber-kill-chain-through.png) [^1]
## out
![Cyber Kill Chain out]({{ site.url }}/assets/images/cyber-kill-chain-out.png) [^1]

[^1]: [unifiedkillchain.com: The-Unified-Kill-Chain.pdf](https://www.unifiedkillchain.com/assets/The-Unified-Kill-Chain.pdf)