---
title: "Windows Forensics Artifacts"
categories: 
- informationsecurity
tags:
- blue team
classes: 
- wide
excerpt: "" 
toc: true
--- 

## Amcache

* The Windows Amcache is a database that tracks how applications interact with Windows for compatibility and performance.
* default location
  * C:\Windows\AppCompat\Programs\Amcache.hve
* path to the location:
  * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache
* forensic values:
  * full file path of the executable
  * The SHA1 hash of the executable
  * Timestamp information (created and last modified, which can be considered the runtime of the executable in some cases)
  * PE properties (header data and PE linker timestamp)
  * File version information (ProductName, CompanyName, Description)
  * install and uninstall timestamps
* can be read with:
  * [AmcacheParser][def1]

## AppCompatCache

* is a Windows component that stores data about application compatibility, helping Windows optimize software performance and security
* location:
  * **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SessionManager\AppCompatCache, AppCompatCache**
* forensic values:
  * Full file path
  * File size
  * The MFT $SI ($Standard_Information) last modified time
  * Cache entry position
  * ShimCache last updated time
  * Process execution flag
* note:
  * only contains entries before the last system shutdown
  * Entries on the current session are stored in memory
* tools:
  * [AppCompatCacheParser][def2]

## prefetch files

* Prefetch files are data caches in Windows that speed up the launch of frequently used applications and improve boot times. Windows manages them automatically, so user intervention is typically unnecessary
* location
  * **C:\Windows\Prefetch\*.pf**
* forensic values:
  * name of the executable file (up to 29 characters)
  * path of the executable file
  * creation, last modified, and last accessed timestamps of the executable file
  * run count of the executable
  * Last run timestamp
  * Additional timestamps for the last seven runtimes
  * Files and directories referenced by the executable during startup
  * Volume information
* tools:
  * [PEcmd][def3]

## Event Logs

* Location
  * Event logs: *C:\Windows\System32\WinEVT\Logs\*.evtx*
  * Registry keys: *HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\EventLog\<channel>\<provider>*
* settings for different types of event logs, like security or application logs
  * *HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\WINEVT\Channels\*
* forensic values
  * Timestamp
  * Event type
  * Event level
  * Source
  * Event ID
  * Opcode
  * Associated user
  * System
  * Message

## UserAssist

* registry key that tracks and stores information about programs executed on the system
  * *HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist*
* Format
  * *{CEBFF5CD-ACE2-4F4F-9178-9926F41749EA}*: Application or Executable File Execution
  * *{F4E57C4B-2036-45F0-A9AB-443BCFE33D9F}*: Shortcut File Execution
  * *{0D6D4F41-2994-4BA0-8FEF-620E43CD2812}*: Internet Explorer version 7
  * *{5E6AB780-7743-11CF-A12B-00AA004AE837}*: Points to the Internet Toolbar
  * *{75048700-EF1F-11D0-9888-006097DEACF9}*: ActiveDesktop
* forensic values:
  * Program ID: A unique identifier for an application or shortcut.
  * Run count: The number of times an application has been launched.
  * Focus count: The number of times an application window has been brought into focus by the user.
  * Focus time: The total time in milliseconds that an application window has been in focus.
  * Last execution time: The timestamp of the most recent execution of an application.

## ShellBags

* are forensic artifacts in Windows that track folder and file access history, providing insight into a user's navigation and interaction with the file system
* forensic values
  * Name of the folder
  * Full path to the folder
  * MFT (Master File Table) entry and sequence number
  * File record number
  * Creation date timestamp
  * Last access timestamp
  * Last modified timestamp
* location
  * *HKEY_CURRENT_USER\Software\Microsoft\Windows\Shell\Bags*
* Tools:
  * SBEcmd

## Recycle Bin

## Analytics

### File permissions

```bash
# Powershell
Get-ACL file.txt

# find hidden stream data
Get-Item -path .\test.txt -stream *
```

# registry

```bash

```

## source

[def1]: https://github.com/EricZimmerman/AmcacheParser
[def2]: https://github.com/EricZimmerman/AppCompatCacheParser
[def3]: https://github.com/EricZimmerman/PECmd
