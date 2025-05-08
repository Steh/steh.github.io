---
title: "Memory Forensics"
categories: 
  - informationsecurity
tags: 
  - memory forensics
  - blue team
classes: 
  - wide
excerpt: ""
toc: true
date: 2022-12-14
---
## What is Memory Forensics

Memory forensics is the analysis of the volatile memory that is in use when a computer is powered on. Computers use dedicated storage devices called Random Access Memory (RAM) to remember what is being performed on the computer at the time. RAM is extremely quick and is the preferred method of storing and accessing data. However, it is limited compared to storage devices such as hard drives. This type of data is volatile because it will be deleted when the computer is powered off. RAM stores data such as your clipboard or unsaved files.[^1]

## Using Volatility

Volatility is an open-source memory forensics toolkit written in Python. Volatility allows us to analyse memory dumps taken from Windows, Linux and Mac OS devices and is an extremely popular tool in memory forensics.[^1]

```bash
## getting os informations from image
python3 vol.py -f image.vmem windows.info

## Exporting files from an process
python3 vol.py -f workstation.vmem windows.dumpfiles --pid 4640
```

### Windows Plugins

* windows.pslist:
  * Lists the processes present in a particular windows memory image
* windows.psscan
  * Scans for processes present in a particular windows memory image
* windows.dumpfiles
  * export the process
* windows.netstat
  * lists all network connections at the time of the capture

## References

* [volatility3: plugins](https://volatility3.readthedocs.io/en/latest/volatility3.plugins.html)
* [volatility3: Windows plugins](https://volatility3.readthedocs.io/en/stable/volatility3.plugins.windows.html)

[^1]: [tryhackme: Advent of Cyber Day 11](https://tryhackme.com/room/adventofcyber4)
