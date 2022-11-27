---
layout: post
title: "Exchange: Postfachberechtigungen anzeigen"
categories: Exchange
tags: ["Exchange", "PowerShell"]
autor: StehSa
--- 

## Alle Benutzer mit Vollzugriff auf diese Mailbox anzeigen
    Get-Mailbox <Mailbox> | Get-MailboxPermission | ? {($_.IsInherited -eq $False) -and ($_.User -notlike "NT AUTHORITY\SELF")} | FT Identity,User,AccessRights -AutoSize
    
## Senden Als berechtigung ausgeben
    Get-Mailbox <Mailbox> | Get-ADPermission | ? {($_.ExtendedRights -like "*send-as*") -and -not ($_.User -like "nt authority\self")} | ft Identity, User

## Stellvertreterzugriff ausgeben
    Get-Mailbox <Mailbox> | ? {$_.GrantSendOnBehalfTo} | ft Alias,GrantSendOnBehalfTo -AutoSize

[cammckenzie.com: powershell-command-to-check-send-as-permissions](https://www.cammckenzie.com/blog/index.php/2012/11/08/powershell-command-to-check-send-as-permissions/)
