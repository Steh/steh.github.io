---
layout: post
title: "Exchange: Postfachberechtigungen anzeigen"
categories: Exchange
tags: ["Exchange", "PowerShell"]
--- 

    # Allgemeine Mailbox Berechtigungen
    Get-Mailbox <Mailbox> | Get-MailboxPermission | Where-Object {($_.IsInherited -eq $False) -and ($_.User -notlike "NT AUTHORITY\SELF")} | FT Identity,User,AccessRights -AutoSize

[cammckenzie.com: powershell-command-to-check-send-as-permissions](https://www.cammckenzie.com/blog/index.php/2012/11/08/powershell-command-to-check-send-as-permissions/)
