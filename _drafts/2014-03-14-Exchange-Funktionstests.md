---
layout: post
title: 'Exchange: Funktionstests der Umgebung'
tagline: "Funktionstests und Fehlersuche in der Exchange Umgebung"
category: Exchange2010
tags: ["Exchange", "Fehlersuche"]
autor: StehSa
---

## Test Cmdlets 
    # User
	Test-ArchiveConnectivity -UserSmtp <USER-E-MAIL>
	
	# ClientAccess-Server
	Test-ActiveSyncConnectivity
	Get-ClientAccessServer | Test-EcpConnectivity  | ft -AutoSize
	Get-ClientAccessServer | Test-ImapConnectivity | ft -AutoSize
	Test-MRSHealth
	Test-OutlookConnectivity -Protocol HTTP | ft -AutoSize
	Test-OutlookConnectivity -Protocol TCP | ft -AutoSize
	Test-OutlookWebServices
	Test-OwaConnectivity
	Test-PopConnectivity
	
	Get-ClientAccessServer | Test-PowerShellConnectivity | ft -AutoSize
	Get-ClientAccessServer | Test-SmtpConnectivity
	Get-ClientAccessServer | Test-WebServicesConnectivity | ft -AutoSize
	Get-ClientAccessServer | Test-PowerShellConnectivity | ft -AutoSize
	
	# Mailbox-Server
	Test-AssistantHealth
	Test-ExchangeSearch
	Test-Mailflow
	Get-MailboxServer | Test-MAPIConnectivity
	Get-MailboxServer | Test-ReplicationHealth | ft -AutoSize
	
	
	# Alle Server
	Get-ExchangeServer | where { $_.AdminDisplayVersion -like "Version 14.3*"} | Test-ServiceHealth
	
	# ??
	Test-SystemHealth
