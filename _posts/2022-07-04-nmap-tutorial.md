---
layout: post
title: "nmap cheat sheet"
categories: [nmap, cheatsheet]
tags: ['cheatsheet', 'nmap']
autor: StehSa
--- 

# nmap cheat sheet
	
	# Legacy Adressrichlinien ausgeben
    Get-EmailAddressPolicy | where {$_.RecipientFilterType –eq “Legacy”}
    Get-EmailAddressPolicy | Format-List Name, *RecipientFilter*, ExchangeVersion

	# Nach 2010 übertragen
	Get-EmailAddressPolicy | Set-EmailAddressPolicy -RecipientFilter <FILTER>
	
	# Listen ausführen
	Get-EmailAddressPolicy | Update-EmailAddressPolicy
	

[Microsoft Hilfeseite zur Migration in Exchange 2010](http://technet.microsoft.com/en-us/library/cc164375.aspx)