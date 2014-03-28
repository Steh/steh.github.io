---
layout: post
title: 'Exchange: Mailbox Ordner und Berechtigungen'
categories: Exchange2010
tags: ['Mailbox-Ordner','Ordner-Berechtigungen']
Autor: StehSa
---

##Ordner einer Mailbox anzeigen

    Get-MailboxFolderStatistics <mailbox> | Select-Object FolderPath

## Ordnerberechtigungen anzeigen

    Get-MailboxFolderPermission <MailboxAlias/OrdnerName> 