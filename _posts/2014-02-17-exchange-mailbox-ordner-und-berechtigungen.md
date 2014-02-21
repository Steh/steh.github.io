---
layout: post
title: 'Exchange: Mailbox Ordner und Berechtigungen'
categories:
- Exchange
- Exchange 2007
- Exchange 2010
- PowerShell
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  _sd_is_markdown: '1'
  sharing_disabled: '1'
  _wpas_done_all: '1'
---
<h1>Ordner einer Mailbox anzeigen</h1>

<pre><code>Get-MailboxFolderStatistics &lt;mailbox&gt; | Select-Object FolderPath  
</code></pre>

<h1>Ordnerberechtigungen anzeigen</h1>

<pre><code>Get-MailboxFolderPermission &lt;MailboxAlias:&lt;OrdnerName&gt;  
</code></pre>
