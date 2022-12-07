---
title: "Nmap scannning"
categories: 
- informationsecurity
tags:
- red team
- nmap
classes: 
- wide
--- 
## scanning types
* **passive scanning**: 
  * "involves scanning a network without directly interacting with the target device"[^1]
  * "is usually carried out through packet capture and analysis tools like Wireshark"[^1]
* **active scanning**:
  * " is a scanning method whereby you scan individual endpoints in an IT network to retrieve more detailed information"
  * "active scan involves sending packets or queries directly to specific assets"

## scanning techniques

## vulnerability scanning
* "vulnerability scanning proactively identifies the network's vulnerabilities in an automated way"
* Tool
  * Nessus
  * Nexpose
  * Greenbone

```bash
#-sC: Performs a script scan using the default set of scripts.
#-sV: Enables version detection, which will detect what versions are running on what port.
nmap -sC -sV xx.xx.xx.xx

# ping scan
nmap -sn xx.xx.xx.xx

# OS Scan
nmap -O xx.xx.xx.xx

# Detecting Services
nmap -sV xx.xx.xx.xx
```

# references
- [Kali.org: nmap Usage Example](https://www.kali.org/tools/nmap/)
- [linux.die.net: nmap(1) - Linux man page](https://linux.die.net/man/1/nmap)

[^1]: https://tryhackme.com/room/adventofcyber4
