---
title: "Splunk and Auditd"
categories: 
- informationsecurity
tags:
- blue team
- Splunk 
- auditd
- detection
classes:
- wide
excerpt: "How to work with splunk and auditd logs" 
---
# show the executet commandline
Auditd decodes the commandline to hex as a security measurement, so you have to convert it back.
You can´t use the datamodel to do it, it doesn´t contains the necessary information.

What you have to do to see the executed commands:
* switch auditd log_format to enriched
* combine all needed Events
* select only the fields you need to reduce workload
* convert the proctitle hex field to ascii
* if you don´t get an result, you should try to filter the subsearches or reduce the timespan of the search

```bash
# combine all eventypes to one Entry
index=auditd_data type="EXECVE"
| join msg a0
    [ search index=auditd_data type="SYSCALL"
    | fields msg host AUID UID Host user key]
| join msg
    [ search index=auditd_data type="PROCTITLE"
    | fields msg proctitle]
``` convert hex to ascii ```
| eval proctitle_ascii = urldecode(replace(replace(proctitle,"([0-9A-F]{2})","%\1"),"%00","%20"))
| Table _time host key AUID UID a0 proctitle_ascii
````
# How does the conversion to ascii is working
* the replace in the middle will add an % infront of every second char
* at first replace . (%00) with an space (%20)
* the url decode command converts the hex to ascii


# references
* [redhat.com: Understanding Audit Log Files](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/security_guide/sec-understanding_audit_log_files)
* [community.splunk.com: How to convert Hex to Ascii in Splunk?](https://community.splunk.com/t5/Splunk-Search/How-to-convert-Hex-to-Ascii-in-Splunk/m-p/189267)
* [Splunk docs: replace](https://docs.splunk.com/Documentation/Splunk/9.0.4/SearchReference/TextFunctions#replace.28X.2CY.2CZ.29)
* [Splunk docs: urldecode](https://docs.splunk.com/Documentation/SCS/current/SearchReference/TextFunctions#urldecode.28.26lt.3Burl.26gt.3B.29)
