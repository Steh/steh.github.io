---
layout: post
title: Exchange: Senden-Als Berechtigungen für Mailbox anzeigen
categories: [Exchange]
tags: []
---
    Get-Mailbox <MAILBOX> | Get-ADPermission | where {($_.ExtendedRights -like "*Send-As*")} | Fl
