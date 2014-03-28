---
layout: post
title: "Exchange: Öffentliche Ordner
category : Exchange
tagline: "Exchange: Öffentliche Ordner mit der PowerShell administrieren"
tags : [Exchange, Öffentliche-Ordner]
---

{% include JB/setup %}

## PowerShell Befehle
	# Alle Ordner Unterhalb des Hauptordners anzeigen
    Get-PublicFolder -GetChildren
	
	# E-Mail aktivierte öffentliche Ordner anzeigen
	Get-MailPublicFolder
	
	# Details über einen Ordner
	Get-PublicFolderStatistics