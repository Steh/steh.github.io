---
title: "Threat Hunt"
categories: 
- informationsecurity
tags:
- blue team
classes: 
- wide
excerpt: "" 
toc: true
--- 
"A threat-hunting hypothesis, much like a scientific hypothesis, is a statement of an idea or explanation to test against data."[1]

# the three threat hunting hypotesis
* Threat intelligence-based
    * relies on indicators of compromise
* Situational awareness-based
    * known as the ‘Crown Jewels Analysis’
    * focus on the most important assets
* Domain expertise-based
    * based on threat hunters expertise
    * is importent to document the lessons learned and teaching those lessons to other members of the team

# types of hunts
* Data-driven
    * are unstructured
    * initiated triggered by a alert
* Intel-driven
    * are informed by threat intelligence
    * differs from the data-driven approach as this hunt is performed proactively and no alerts are triggered
* Entity-driven
    * focus on critical intellectual property and assets belonging to an organization that are likely to be targeted
    * Examples include R&D servers, domain controllers, or system administrator accounts
* TTP-driven
    * focusing on an adversary's tactics, techniques and procedures
    * Identifying and understanding the tools used by threat actors, alongside their motivations
* Hybrid
    * combine all the methods previously mentioned 
    * For example, utilizing the TTP-driven and entity-driven approaches to better understand a threat actor's motivations and most common targets, can help identify the organization's most vulnerable assets.

# references
* [^1](ImmersiveLabs: Threat Hunting Theory)[https://immersivelabs.online/v2/labs/threat-hunt-theory-hypothesis-creation/role/introduction-to-cyber-threat-intelligence/series/threat-hunting-theory]
* (ImmersiveLabs: Threat Hunting Theory - Types of Hunt)[https://immersivelabs.online/v2/labs/threat-hunt-theory-types-of-hunt-bdb9f2af-b889-425f-a96c-9816ad3ae052/role/introduction-to-cyber-threat-intelligence/]
