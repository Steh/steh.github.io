---
title: "Log Analysis"
categories: 
- informationsecurity
tags:
- blue team
classes: 
- wide
excerpt: "" 
toc: true
--- 

* Logs are recorded events or transactions within a system, device, or application.

## Types of Logs

    Application Logs: Messages from specific applications, providing insights into their status, errors, warnings, and other operational details.
    Audit Logs: Events, actions, and changes occurring within a system or application, providing a history of user activities and system behavior.
    Security Logs: Security-related events like logins, permission alterations, firewall activities, and other actions impacting system security.
    Server Logs: System logs, event logs, error logs, and access logs, each offering distinct information about server operations.
    System Logs: Kernel activities, system errors, boot sequences, and hardware status, aiding in diagnosing system issues.
    Network Logs: Communication and activity within a network, capturing information about events, connections, and data transfers.
    Database Logs: Activities within a database system, such as queries performed, actions, and updates.
    Web Server Logs: Requests processed by web servers, including URLs, source IP addresses, request types, response codes, and more.

## Investigation Theory

* Create a Timeline
    * understanding the sequence of events within systems, devices, and applications
    * chronological representation of the logged events, ordered based on their occurrence
* Timestamp
    * 
* Super Timeline
    * provide a comprehensive view of events across different systems, devices, and applications, allowing analysts to understand the sequence of events holistically
    * Tool: https://plaso.readthedocs.io/en/latest/ 
* External Research
    * When analyzing a log file, we can search for the presence of threat intelligence
    * Website: https://threatfox.abuse.ch/

## Common Log File Locations

    Web Servers:
        Nginx:
            Access Logs: /var/log/nginx/access.log
            Error Logs: /var/log/nginx/error.log
        Apache:
            Access Logs: /var/log/apache2/access.log
            Error Logs: /var/log/apache2/error.log

    Databases:
        MySQL:
            Error Logs: /var/log/mysql/error.log
        PostgreSQL:
            Error and Activity Logs: /var/log/postgresql/postgresql-{version}-main.log

    Web Applications:
        PHP:
            Error Logs: /var/log/php/error.log

    Operating Systems:
        Linux:
            General System Logs: /var/log/syslog
            Authentication Logs: /var/log/auth.log

    Firewalls and IDS/IPS:
        iptables:
            Firewall Logs: /var/log/iptables.log
        Snort:
            Snort Logs: /var/log/snort/

## Detection Engineering

    Abnormal Behaviour
        any actions or activities conducted by users that deviate from their typical or expected behavior (baselining)
    Multiple failed login attempts
        Unusually high numbers of failed logins within a short time may indicate a brute-force attack.
    Unusual login times
        Login events outside the user's typical access hours or patterns might signal unauthorized access or compromised accounts.
    Geographic anomalies
        Login events from IP addresses in countries the user does not usually access can indicate potential account compromise or suspicious activity.
        In addition, simultaneous logins from different geographic locations (or indications of impossible travel) may suggest account sharing or unauthorized access.
    Frequent password changes
        Log events indicating that a user's password has been changed frequently in a short period may suggest an attempt to hide unauthorized access or take over an account.
    Unusual user-agent strings
        In the context of HTTP traffic logs, requests from users with uncommon user-agent strings that deviate from their typical browser may indicate automated attacks or malicious activities.
        For example, by default, the Nmap scanner will log a user agent containing "Nmap Scripting Engine." The Hydra brute-forcing tool, by default, will include "(Hydra)" in its user-agent. These indicators can be useful in log files to detect potential malicious activity.
    SQL Injection
        Look for unusual or malformed SQL queries
    Cross-Site Scripting (XSS)
        allow attackers to inject malicious scripts into web pages
    Path Traversal
        allows attackers to access files and directories outside a web application's intended directory structure

## Log Analysis

### command line

```bash
# cat command (short for "concatenate") 
cat access.log

# grep text search tool 
## -n add line count
## -c count matched entries
grep "error" access.log

# less allows you to view the file's data page by page (q for exit)
less access.log

# tail viewing the end of files
## -f follow file live
## -n line count to show
tail -f -n 5 access.log

# wc
## -l linecount
## -w wordcount
wc access.log

# cut
## -d delimiter
## -f field number
cut -d ' ' -f 1 access.log

# sort
## -n ascending
## -r reverse
cat access.log | sort

# uniq removes adjacent duplicate lines from sorted input
cat access.log | sort | uniq


```

## source

* [Text][def]

[def]: https://tryhackme.com/room/introtologanalysis
