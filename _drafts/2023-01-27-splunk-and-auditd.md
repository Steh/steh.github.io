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
Auditd decodes the commandline to hex, so you have to convert it.
You can´t use the datamodel to do it, it doesn´t contains the information.

What you have to do:
* switch auditd log_format to enriched
* combine all needed Events
* select only the fields you need to reduce workload
* convert the proctitle hex field to asci

```bash
# combine all eventypes to one Entry
index=auditd_data type="EXECVE"
| join msg a0
    [ search index=auditd_data type="SYSCALL"
    | fields msg host AUID UID Host user key]
| join msg
    [ search index=auditd_data type="PROCTITLE"
    | fields msg proctitle]
| eval proctitle_asci = urldecode(replace(replace(proctitle,"([0-9A-F]{2})","%\1"),"%00","%20"))
| Table _time host key AUID UID a0 proctitle_asci
```

# references
* (redhat.com: Understanding Audit Log Files)[https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/security_guide/sec-understanding_audit_log_files]
* (community.splunk.com: How to convert Hex to Ascii in Splunk?)[https://community.splunk.com/t5/Splunk-Search/How-to-convert-Hex-to-Ascii-in-Splunk/m-p/189267]
