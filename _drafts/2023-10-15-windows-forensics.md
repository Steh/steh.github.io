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

## source

[def1]: https://github.com/EricZimmerman/AmcacheParser
[def2]: https://github.com/EricZimmerman/AppCompatCacheParser
[def3]: https://github.com/EricZimmerman/PECmd
