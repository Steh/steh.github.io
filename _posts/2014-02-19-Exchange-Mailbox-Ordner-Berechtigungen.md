---
type: post
layout: post
title: "Exchange: Mailbox Ordner und Berechtigungen anzeigen"
description: ""
category: Exchange 
tags: ["Exchange", "Get-MailboxFolderStatistics", "Ordnerberechtigungen"]
---


Ordner einer Mailbox anzeigen

    Get-MailboxFolderStatistics <mailbox> | Select-Object FolderPath

Ordnerberechtigungen anzeigen

    Get-MailboxFolderPermission <MailboxAlias>:<OrdnerName> 
