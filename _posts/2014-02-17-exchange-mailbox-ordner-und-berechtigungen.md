---
layout: post
title: 'Exchange: Mailbox Ordner und Berechtigungen'
categories: Exchange
tags: []
type: post
---

{% include JB/setup %}

##Ordner einer Mailbox anzeigen

    Get-MailboxFolderStatistics <mailbox> | Select-Object FolderPath

## Ordnerberechtigungen anzeigen

    Get-MailboxFolderPermission <MailboxAlias/OrdnerName> 