---
title: "Splunk: building better notables"
categories: 
- informationsecurity
tags:
- blue team
- splunk
classes: 
- wide
toc: true
excerpt: "A Few Tipps to build better notables in Splunk ES"
--- 

Notables in Splunk Enterprise Security (ES) are records of security-related events that require further investigation or action by security analysts. Notables are created by rules in Splunk ES that detect suspicious or anomalous behavior in the security data.

## Contributing Events

* add a search that will show you the search results that lead to the notables
* By adding the search to the notable field "Drill-down Search" you cant see the events

## Add "Next Steps" descriptions

* add Instructions to the notable so that everybody knows what to do
* "Next Steps" in the notable

## Convert your searches to Correlation Searches

* Correlation Searches have more possiblitys to investigate events
* add the following to your search and Reload all endpoints
  * `https://<splunk-ip>:<port>/en-GB/debug/refresh`
* to transform a search you have to add the following parameters: [^1]

```bash
# add the following lines to "savedsearches.conf" search
action.correlationsearch = 0
action.correlationsearch.enabled = 1
action.correlationsearch.label = "rule_name"
description = "description"
```

## data enrichment with asset details

* enrich your assets with additional informations like Hostnames or departments for user
* this can be done with the Asset & Identity Framework [^2]

## Customise your "Incident Review" Dashboard

### Change Table Attributes

* change the "table Attributes" to "Incident Review"
  * `Enterprise Security -> Configure -> Incident Management -> Incident Review Settings`
  * add your values to "Incident Review - Table Attributes"

### Use saved filters for faster filtering

* Change the default filter view to your needs
* Set your filters and hit "Save new filters"

### Add more data to event details view

* to add data to a notable you need to extract the data from the search and add it to the notable
* extract the field:
  * `correlation search -> notable -> Asset Extraction`
* add the field to "Incident Review"
  * `Enterprise Security -> Configure -> Incident Management -> Incident Review Settings`
  * add your values to "Incident Review - Event Attributes"

## references

* [Configure correlation searches](https://docs.splunk.com/Documentation/PCI/5.1.0/Install/Correlationsearches)

[^1]: [https://docs.splunk.com/Documentation/PCI/5.1.1/Install/Correlationsearches#Changes_you_have_to_make_after_upgrade](correlationsearches.conf parameter translation to savedsearches.conf)
[^2]: [https://www.splunk.com/en_us/blog/security/asset-identity-for-splunk-enterprise-security-part-1-contextualizing-systems.html](Asset & Identity for Splunk Enterprise Security - Part 1: Contextualizing Systems)
