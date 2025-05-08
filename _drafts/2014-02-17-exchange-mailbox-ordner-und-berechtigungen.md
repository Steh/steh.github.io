---
layout: post
title: "Exchange: Mailbox Ordner und Berechtigungen"
categories: 
  - Exchange
tags: 
  - Mailbox-Ordner
  - Ordner-Berechtigungen
author: StehSa
excerpt: "How to view and manage mailbox folder permissions in Exchange."
---

##Ordner einer Mailbox anzeigen

    Get-MailboxFolderStatistics <mailbox> | Select-Object FolderPath

## Ordnerberechtigungen anzeigen
Im FolderPath muss '/' durch '\' ersetzt werden

z.B. **stehsa:\Posteingang**
    
    Get-MailboxFolderPermission <MailboxAlias>:<FolderPath>
