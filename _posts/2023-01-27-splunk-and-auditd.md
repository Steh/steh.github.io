---
title: "Splunk and Auditd"
categories: 
  - splunk
tags:
  - blue team
  - splunk
  - auditd
  - detection
  - informationsecurity
classes: 
  - wide
excerpt: "How to work with auditd and splunk"
toc: true
date: 2023-01-27
---

* requirements:
  * change the auditd log_format from *raw* to *enriched*
    * */etc/audit/auditd.conf*
  * Install the [Splunk Add-on for Linux][def]
  * change the sourcetype to: *linux:audit:enriched* or *linux:audit*
    * (i haven´d checked at the moment which one works better)

## combine the auditd log types (EXECVE|SYSCALL|PROCTITLE)

* switch auditd log_format to 'enriched' to add username to logging
  * "/etc/auditd/auditd.conf" -> log_format=ENRICHED
* combine all events
* select the fields you need to reduce workload
* if you don´t get any results, you should try to filter the subsearches or reduce the timespan of the search

```bash
index=auditd_data type="EXECVE"
| join msg a0
    [ search index=auditd_data type="SYSCALL"
    | fields msg host AUID UID Host user key]
| join msg
    [ search index=auditd_data type="PROCTITLE"
    | fields msg proctitle]
| Table _time host key AUID UID a0 proctitle
```

## convert the proctile field to ascii

Auditd decodes the output to hex, so you have to convert it back to ascii.

1. add an % bevor every char pair to create an URL-encoded String  
1. replace . (%00) with an space (%20)
1. convert the url encoded string to ascii

```bash
# combine all eventypes to one Entry
index=* sourcetype=linux:audit:enriched type="PROCTITLE"
``` convert hex to ascii ```
| eval proctitle_ascii = urldecode(replace(replace(proctitle,"([0-9A-F]{2})","%\1"),"%00","%20"))
```

## references

* [redhat.com: Understanding Audit Log Files](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/security_guide/sec-understanding_audit_log_files)
* [community.splunk.com: How to convert Hex to Ascii in Splunk?](https://community.splunk.com/t5/Splunk-Search/How-to-convert-Hex-to-Ascii-in-Splunk/m-p/189267)
* [Splunk docs: replace](https://docs.splunk.com/Documentation/Splunk/9.0.4/SearchReference/TextFunctions#replace.28X.2CY.2CZ.29)
* [Splunk docs: urldecode](https://docs.splunk.com/Documentation/SCS/current/SearchReference/TextFunctions#urldecode.28.26lt.3Burl.26gt.3B.29)


[def]: https://splunkbase.splunk.com/app/3412