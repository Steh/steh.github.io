---
title: "Network Forensics"
categories: 
  - informationsecurity
tags:
  - blue team
  - thm
  - network forensics
  - networkminer
classes: 
  - wide
excerpt: "Network forensics analyzes network traffic to uncover evidence of security incidents, aiding in incident response and prevention."
toc: true
date: 2023-04-11
---
* Questions an investogation tries to answer:
  * Who (Source IP and port)
  * What (Data/payload)
  * Where (Destination IP and port)
  * When (Time and data)
  * Why (How/What happened)

* use cases
  * *Network discovery*: Discovering the network to overview connected devices, rogue hosts and network load.
  * *Packets reassembling*: Reassembling the packets to investigate the traffic flow. This use case is helpful in unencrypted traffic flows.
  * *Data leakage detection*: Reviewing packet transfer rates for each host and destination address helps detect possible data leakage.
  * *Anomaly and malicious activity detection*: Reviewing overall network load by focusing on used ports, source and destination addresses, and data helps detect possible malicious activities along with vulnerabilities. This use case covers the correlation of indicators and hypotheses as well.
  * *Policy/Regulation compliance control*: Reviewing overall network behaviour helps detect policy/regulation compliance.

* NetworkMiner in a Nutshell
  * Traffic sniffing
    * It can intercept the traffic, sniff it, and collect and log packets that pass through the network.
  * Parsing PCAP files
    * It can parse pcap files and show the content of the packets in detail.
  * Protocol analysis
    * It can identify the used protocols from the parsed pcap file.
  * OS fingerprinting
    * It can identify the used OS by reading the pcap file. This feature strongly relies on Satori and p0f.
  * File Extraction
    * It can extract images, HTML files and emails from the parsed pcap file.
  * Credential grabbing
    * It can extract credentials from the parsed pcap file.
  * Clear text keyword parsing
    * It can extract cleartext keywords and strings from the parsed pcap file.

## source

* [TryHackMe: NetworkMiner](https://tryhackme.com/room/networkminer)
* [TryHackMe: Room Write Up](https://medium.com/@haircutfish/tryhackme-networkminer-task-1-through-task-4-527779fb49b7)
* [NetworkMiner](https://www.netresec.com/?page=NetworkMiner)
