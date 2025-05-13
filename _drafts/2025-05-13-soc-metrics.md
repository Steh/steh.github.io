---
title: "SOC Metrics"
categories: 
- informationsecurity
tags:
- blue team
classes: 
- wide
excerpt: "" 
toc: true
--- 

## Core Metrics

Alerts Count 	AC = Total Count of Alerts Received 	Overall load of SOC analysts
False Positive Rate 	FPR = False Positives / Total Alerts 	Level of noise in the alerts
Alert Escalation Rate 	AER = Escalated Alerts / Total Alerts 	Experience of L1 analysts
Threat Detection Rate 	TDR = Detected Threats / Total Threats 	Reliability of the SOC team

## triage metrics

Metric 	Common SLA 	Description
SOC Team Availability 	24/7 	Working schedule of the SOC team, often Monday-Friday (8/5) or 24/7 mode
Mean Time to Detect (MTTD) 	5 minutes 	Average time between the attack and its detection by SOC tools
Mean Time to Acknowledge (MTTA) 	10 minutes 	Average time for L1 analysts to start triage of the new alert
Mean Time to Respond (MTTR) 	60 minutes 	Average time taken by SOC to actually stop the breach from spreading

## some reference metrics

False Positive Rate
over 80% 	Your team receives too much noise in the alerts. Try to:

1. Exclude trusted activities like system updates from your EDR or SIEM detection rules
2. Consider automating alert triage for most common alerts using SOAR or custom scripts
Mean Time to Detect
over 30 min 	Your team detects a threat with a high delay. Try to:

1. Contact SOC engineers to make the detection rules run faster or with a higher rate
2. Check if SIEM logs are collected in real-time, without a 10-minute delay
Mean Time to Acknowledge
over 30 min 	L1 analysts start alert triage with a high delay. Try to:

1. Ensure the analysts are notified in real-time when a new alert appears
2. Try to evenly distribute alerts in the queue between the analysts on shift
Mean Time to Respond
over 4 hours 	SOC team can't stop the breach in time. Try to:

1. As L1, make everything possible to quickly escalate the threats to L2
2. Ensure your team has documented what to do during different attack scenarios

## source

* [Text][def]

[def]: https://tryhackme.com/room/socmetricsobjectives
