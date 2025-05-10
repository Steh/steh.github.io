---
title: "Splunk: CTI Framework"
categories: 
- informationsecurity
tags:
- blue team
classes: 
- wide
excerpt: "An overview of Splunk's Cyber Threat Intelligence (CTI) framework and its applications in information security."
toc: true
---

## Introduction

Splunk's Cyber Threat Intelligence (CTI) framework helps security teams integrate, normalize, and operationalize threat intelligence to detect and respond to threats effectively.

## Key Features

- **Integration**: Ingest multiple threat feeds (open-source, commercial, or custom).
- **Normalization**: Standardize data formats for easier analysis.
- **Correlation**: Match IOCs with internal logs to identify threats.
- **Automation**: Configure alerts and workflows for faster response.
- **Visualization**: Use dashboards to track trends and prioritize threats.

## Integrating Threat Intelligence Sources

1. Navigate to **Settings > Threat Intelligence** in Splunk Enterprise Security.
2. Add a new feed by specifying the source URL, authentication details, and format (e.g., STIX, JSON, CSV).
3. Enable automatic updates to keep the feed current.

## Querying IOCs with SPL

Use the following SPL queries to search for IOCs in your environment:

- **Search for IPs**:

```spl
| inputlookup threatintel_by_ip 
| search ip="192.168.1.1"
```

- **Search for Domains**:

```spl
| inputlookup threatintel_by_domain 
| search domain="malicious.com"
```

- **Correlate IOCs with Logs**:

```spl
index=security_logs 
[| inputlookup threatintel_by_ip | fields ip]
```

## References

- [Threat Intelligence framework in Splunk ES][https://dev.splunk.com/enterprise/docs/devtools/enterprisesecurity/threatintelligenceframework/]
- [Using threat intelligence in Splunk Enterprise Security ][https://lantern.splunk.com/Security/UCE/Guided_Insights/Threat_intelligence/Using_threat_intelligence_in_Splunk_Enterprise_Security]
- [What is Cyber Threat Intelligence? ][https://www.splunk.com/en_us/blog/learn/what-is-cyber-threat-intelligence.html]
- [Indicators of Compromise (IoCs): An Introductory Guide](https://www.splunk.com/en_us/blog/learn/ioc-indicators-of-compromise.html)
