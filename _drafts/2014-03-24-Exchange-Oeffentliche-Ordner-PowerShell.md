---
layout: post
title: "Exchange: Oeffentliche Ordner PowerShell"
category : Exchange2010
tagline: "Exchange: Oeffentliche Ordner mit der PowerShell administrieren"
tags : [Exchange, Oeffentliche-Ordner]
autor: StehSa
---

## PowerShell Befehle
	# Alle Ordner Unterhalb des Hauptordners anzeigen
	Get-PublicFolder -GetChildren
	
	# E-Mail aktivierte öffentliche Ordner anzeigen
	Get-MailPublicFolder
	
	# Details über einen Ordner
	Get-PublicFolderStatistics
