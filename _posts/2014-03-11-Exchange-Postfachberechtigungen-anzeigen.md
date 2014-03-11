---
layout: post
title: "Exchange: Postfachberechtigungen anzeigen"
categories: Exchange
tags: ["Exchange", "PowerShell"]
--- 

    # Allgemeine Mailbox Berechtigungen
    Get-Mailbox <Mailbox> | Get-MailboxPermission | ? {($_.IsInherited -eq $False) -and ($_.User -notlike "NT AUTHORITY\SELF")} | FT Identity,User,AccessRights -AutoSize
    
    # Senden Als ausgeben
    Get-Mailbox sander2 | Get-ADPermission | ? {($_.ExtendedRights -like "*send-as*") -and -not ($_.User -like "nt authority\self")} | ft Identity, User

[cammckenzie.com: powershell-command-to-check-send-as-permissions](https://www.cammckenzie.com/blog/index.php/2012/11/08/powershell-command-to-check-send-as-permissions/)
