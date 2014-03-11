---
layout: post
title: "Exchange: Postfachberechtigungen anzeigen"
categories: Exchange
tags: ["Exchange", "PowerShell"]
--- 

    # Allgemeine Mailbox Berechtigungen
    Get-Mailbox <Mailbox> | Get-MailboxPermission | Where-Object {($_.IsInherited -eq $False) -and ($_.User -notlike "NT AUTHORITY\SELF")} | FT Identity,User,AccessRights -AutoSize

[Microsoft Hilfeseite zur Migration in Exchange 2010](http://technet.microsoft.com/en-us/library/cc164375.aspx)
