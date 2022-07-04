---
layout: post
title: 'Exchange 2010: Mailbox verschieben schlägt fehl'
tagline: '[MapiExceptionNoSupport]'
categories: Exchange2010
tags: []
autor: StehSa
---
Verschieben von Mailboxen innerhalb einer 2010 Umgebung schlägt fehl.

## Lösung

<ul>
<li><p>Problem ist das im Kalender keine Berechtigungen hinterlegt sind</p></li>
<li><p><a href="http://steh-blog.de/wp-content/uploads/2014/02/mailboxmove_failed_right.png"><img src="http://steh-blog.de/wp-content/uploads/2014/02/mailboxmove_failed_right-256x300.png" alt="mailboxmove_failed_right" width="256" height="300" /></a></p></li>
<li><p>also ExFolders Öffnen auf den Kalender gehen und die Rechte <strong>ZURÜCKSETZTEN</strong></p></li>
</ul>

<pre><code>Mailbox -&gt; Top of Information Store -&gt; Kalender  
</code></pre>

<ul>
<li><p><a href="http://steh-blog.de/wp-content/uploads/2014/02/mailboxmove_failed_right1.png"><img src="http://steh-blog.de/wp-content/uploads/2014/02/mailboxmove_failed_right1.png" alt="mailboxmove_failed_right1" width="201" height="199" /></a></p></li>
<li><p>Nun sollten die rechte gesetzt sein und das verschieben funktionieren</p></li>
</ul>

## Fehlermeldung

	[PS] C:&gt;Get-MoveRequest &lt;mailbox&gt; | Get-MoveRequestStatistics | fl  
	....  
	FailureCode : -2147221246  
	FailureType : MapiExceptionNoSupport  
	FailureSide : Target  
	Message : Fehler: MapiExceptionNoSupport: IExchangeFastTransferEx.TransferBuffer failed (hr=0x80040102, ec=-2147221246)  
	Diagnostic context:  
	Lid: 55847 EMSMDBPOOL.EcPoolSessionDoRpc called [length=4115]  
	Lid: 43559 EMSMDBPOOL.EcPoolSessionDoRpc returned [ec=0x0][length=689][latency=31]  
	Lid: 23226 ---| ROP Parse Start ---|  
	Lid: 27962 ROP: ropFXDstCopyConfig [83]  
	Lid: 27962 ROP: ropTellVersion [134]  
	Lid: 27962 ROP: ropFXDstPutBufferEx [157]  
	Lid: 17082 ROP Error: 0x80040102  
	Lid: 31329  
	Lid: 21921 StoreEc: 0x80040102  
	Lid: 27962 ROP: ropExtendedError [250]  
	Lid: 1494 ---|- Remote Context Beg ---|-  
	Lid: 1238 Remote Context Overflow  
	Lid: 25008 dwParam: 0x6  
	Lid: 24932  
	Lid: 4367 StoreEc: 0x80040102  
	Lid: 7695 StoreEc: 0x80040102  
	Lid: 19936  
	Lid: 4559 StoreEc: 0x80040102  
	Lid: 21802  
	Lid: 19994 StoreEc: 0x80040102  
	Lid: 20202  
	Lid: 3305 StoreEc: 0x80040102  
	Lid: 32762 dwParam: 0xE080003  
	Lid: 32762 dwParam: 0xE230003  
	Lid: 32762 dwParam: 0xE270102  
	Lid: 32762 dwParam: 0xE580102  
	Lid: 32762 dwParam: 0xE590102  
	Lid: 32762 dwParam: 0xF000102  
	Lid: 32762 dwParam: 0xFF40003  
	Lid: 32762 dwParam: 0x10F4000B  
	Lid: 32762 dwParam: 0x10F5000B  
	Lid: 32762 dwParam: 0x10F6000B  
	Lid: 32762 dwParam: 0x300184B0  
	Lid: 32762 dwParam: 0x300484B0  
	Lid: 32762 dwParam: 0x301D0003  
	Lid: 32762 dwParam: 0x3FE4000B  
	Lid: 32762 dwParam: 0x3FE70003  
	Lid: 32762 dwParam: 0x3FE5000B  
	Lid: 26346  
	Lid: 4073 StoreEc: 0x80040102  
	Lid: 28570 StoreEc: 0x80040102  
	Lid: 29738  
	Lid: 3401 StoreEc: 0x80040102  
	Lid: 1750 ---|- Remote Context End ---|-  
	Lid: 26849  
	Lid: 21817 ROP Failure: 0x80040102  
	Lid: 22630

## Quellen

<p><a href="http://www.msxfaq.de/admin/mbrechte.htm" title="http://www.msxfaq.de/admin/mbrechte.htm">MSXFfaq: Rechte auf Postfächer</a></p>
