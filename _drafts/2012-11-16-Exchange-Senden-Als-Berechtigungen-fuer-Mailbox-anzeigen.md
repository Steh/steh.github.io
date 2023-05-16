---
layout: post
title: Exchange Senden-Als Berechtigungen für Mailbox anzeigen
categories: Exchange
---
	Get-Mailbox <MAILBOX> | Get-ADPermission | where {($_.ExtendedRights -like "*Send-As*")} | Fl
