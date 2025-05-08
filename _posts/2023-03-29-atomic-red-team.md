---
title: "Atomic Red Team"
categories: 
  - informationsecurity
tags:
  - blue team
  - red team
  - windows
  - atomic red team
  - attack range
classes: 
  - wide
excerpt: "Atomic Red Team is an open-source project that provides a framework for performing security testing and threat emulation."
toc: true
date: 2023-03-29
---

## installation

```bash
# PowerShell
Import-Module "invoke-atomicredteam\Invoke-AtomicRedTeam.psd1" -Force
$PSDefaultParameterValues = @{"Invoke-AtomicTest:PathToAtomicsFolder"="AtomicRedTeam\atomics"}
```

## How to use

```bash
# get requirements
Invoke-AtomicTest T1127 -GetPrereqs

# get briefdetails
Invoke-AtomicTest T1127 -ShowDetailsBrief

# get details
Invoke-AtomicTest T1127 -ShowDetails

# execute tests
Invoke-AtomicTest T1127 -TestNumbers 1,2

# cleanup after execution
Invoke-AtomicTest T1127 -TestNumbers 1,2 -cleanup
```

## create rules via gui

```powershell
# start gui
Start-AtomicGui

# view
http://localhost:8487/home
```

## Emulating an Attack

```powershell
# view if tests exist
ls C:\Tools\AtomicRedTeam\atomics | Where-Object Name -Match "T1566.001|T1203|T1059.003|T1083|T1082|T1016|T1049|T1007|T1087.001"

# show details
'T1566.001','T1059.003','T1083','T1082','T1016','T1049','T1007','T1087.001' | ForEach-Object {echo "Enumerating $_"; Invoke-AtomicTest $_ -ShowDetailsBrief }

# test Prerequirements
'T1566.001','T1059.003','T1083','T1082','T1016','T1049','T1007','T1087.001' | ForEach-Object {echo "Enumerating $_"; Invoke-AtomicTest $_ -CheckPrereqs }
```

## Searching for Technique on ATT&CK Navigator

* [ATT&CK Navigator](https://mitre-attack.github.io/attack-navigator/)

## sources

* [List of Atomics to use][def]
* [TryHackMe: Atomic Red Team][def2]

[def]: https://atomicredteam.io/atomics/#collection
[def2]: https://tryhackme.com/room/atomicredteam
