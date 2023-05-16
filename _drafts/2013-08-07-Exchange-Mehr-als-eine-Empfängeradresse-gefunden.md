---
layout: post
title: 'Exchange: Mehr als eine Empfängeradresse gefunden'
categories: Exchange
tags: 
Autor: Steh Sa
---
## Fehlermeldung

    More than one Active Directory object is configured with the recipient address IMCAEX-_O=Firma_OU=GRUPPE_cn=Recipients_cn=Steh@lalala.de . 
    Messages to this recipient will be deferred until the configuration is corrected in Active Directory.
    
Fehlermeldung im MessageTracking

    420 4.2.0 Resolver.ADR.Ambigous; ambigous address

## Doppelte Empfänger finden
    vorher:     IMCAEX-_O=Firma_OU=GRUPPE_cn=Recipients_cn=Steh@lalala.de 
    hinterher:  /O=Firma/OU=Gruppe/cn=Recipients/cn=Steh

Empfänger suchen
    Get-Recipient \O=Firma\OU=Gruppe\cn=Recipients\cn=Steh

## Bereinigen
Open ADSI Edit an navigate to the User you want to change:

<a href="http://steh-blog.de/wp-content/uploads/2013/08/adsiedit-suche.png"><img src="http://steh-blog.de/wp-content/uploads/2013/08/adsiedit-suche-300x295.png" alt="adsiedit-suche" width="300" height="295" class="alignnone size-medium wp-image-846" /></a>

Organizational Unit from desired user

Now you have to change the usern LegacyExchangeDN to an <strong>unique</strong> one.
