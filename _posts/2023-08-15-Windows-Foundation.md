---
title: "Windows Foundation"
categories: 
- informationsecurity
tags:
- blue team
classes: 
- wide
excerpt: "Some basics to better understand the how windows works"
toc: true
--- 

## Processes

* are created from the execution of an application
* an application can obtain one or more processes
* Example default processes:
  * MsMpEng (Microsoft Defender)
  * wininit (keyboard and mouse)
  * lsass (credential storage)
* Applications to observe processes
  * [ProcessHacker2][def2]
  * [ProcessExpolorer][def3]
  * [Procmon][def4]
* [Microsoft: About Processes and Threads][def1]

### Components

* Private Virtual Address Space
  * Virtual memory addresses that the process is allocated.
* Executable Program
  * Defines code and data stored in the virtual address space.
* Open Handles
  * Defines handles to system resources accessible to the process.
* Security Context
  * The access token defines the user, security groups, privileges, and other security information.
* Process ID
  * Unique numerical identifier of the process.
* Threads
  * Section of a process scheduled for execution.

### Process in virtual address space

* Code
  * Code to be executed by the process.
* Global Variables
  * Stored variables.
* Process Heap
  * Defines the heap where data is stored.
* Process Resources
  * Defines further resources of the process.
* Environment Block
  * Data structure to define process information.

## Threads

* "A thread is the entity within a process that can be scheduled for execution. All threads of a process share its virtual address space and system resources"
* "controlling the execution of a process"

* Thead data and values
  * Stack
    * All data relevant and specific to the thread (exceptions, procedure calls, etc.)
  * Thread Local Storage
    * Pointers for allocating storage to a unique data environment
  * Stack Argument
    * Unique value assigned to each thread
  * Context Structure
    * Holds machine register values maintained by the kernel

## Virtual Memory

* "The virtual address space for a process is the set of virtual memory addresses that it can use. The address space for each process is private and cannot be accessed by other processes unless it is shared."
  * [Microsoft: Virtual Address Space (Memory Management)][def5]
* Virtual memory provides each process with a private virtual address space
* A memory manager is used to translate virtual addresses to physical addresses

## Dynamic Link Libraries

* "a library that contains code and data that can be used by more than one program at the same time"
* "helps promote modularization of code, code reuse, efficient memory usage, and reduced disk space. So, the operating system and the programs load faster, run faster, and take less disk space on the computer."
* [Microsoft: What is a DLL][def6]
* DLLs are assigned as dependencys
* attackers can alter DLLs to change the application behaviour
* writen in c++

## Portable Executable Format

* Portable Executable (PE) format defines the information about the executable and stored data
* consist of
  * Portable Executable (PE)
  * Common Object File Format (COFF)
*
* PE
  * most commonly seen in hex dump of executable
  * components:
    * DOS Header
      * "MZ"
      * defines file format
    * DOS Stub
      * "This program cannot be run in DOS mode"
      * a programm that runs by default, prints a compatibility message
    * PE File Header
      * starts with "PE"
      * Defines the format of the file, contains the signature and image file header, and other information headers
    * Image Optional Header
      * important part of PE File Header
    * Data Dictionaries
      * part of Image Optional Header
      * pointto the image data directory structure
    * Section Table
      * define the available sections and information in the image
      * store the contents of the file, such as code, imports and data

    * Sections
      * .text
        * Contains executable code and entry point
      * .data
        * Contains initialized data (strings, variables, etc.)
      * .rdata or .idata
        * Contains imports (Windows API) and DLLs.
      * .reloc
        * Contains relocation information
      * .rsrc
        * Contains application resources (images, etc.)
      * .debug
        * Contains debug information

## source

* [TryHackMe: Windows Internals][def]
* [TryHackMe: writeup][def7]

[def]: https://tryhackme.com/room/windowsinternals
[def1]: https://docs.microsoft.com/en-us/windows/win32/procthread/about-processes-and-threads
[def2]: https://github.com/processhacker/processhacker
[def3]: https://docs.microsoft.com/en-us/sysinternals/downloads/process-explorer
[def4]: https://docs.microsoft.com/en-us/sysinternals/downloads/procmon
[def5]: https://docs.microsoft.com/en-us/windows/win32/memory/virtual-address-space
[def6]: https://learn.microsoft.com/en-us/troubleshoot/windows-client/deployment/dynamic-link-library
[def7]: https://github.com/jesusgavancho/TryHackMe_and_HackTheBox/blob/master/Windows%20Internals.md
