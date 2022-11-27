---
layout: post
categories: PowerShell
title: 'PowerShell: Befehle auf anderen Computern ausführen'
tagline: 'Anzeigen und wieder einbinden'
tags: [PowerShell, Remote]
autor: StehSa
---
## PowerShell Befehl

	Invoke-Command -ComputerName <Server1>,<Server2>
	-Command { (get-childitem env:COMPUTERNAME).value }

## Quelle
[windowsitpro.com: Creating Remote Sessions...](http://windowsitpro.com/scripting/creating-remote-sessions-powershell-20)
