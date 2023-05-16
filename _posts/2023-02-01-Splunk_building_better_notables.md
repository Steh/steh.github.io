---
title: "Building Better Notables in Splunk ES"
categories: 
- information security
tags:
- blue team
- splunk
- splunk enterprise security
classes: 
- wide
toc: true
excerpt: "Tips for optimizing notables in Splunk Enterprise Security"
--- 

Notables in Splunk Enterprise Security (ES) are records of security-related events that require further investigation or action by security analysts. Notables are created by rules in Splunk ES that detect suspicious or anomalous behavior in the security data.

## Contributing Events

- Add a search to show the search results leading to the notables.
- Use the "Drill-down Search" field in the notable to view the events.

## Add "Next Steps" Descriptions

- Include clear instructions in the notables to guide the next steps.
- Utilize the "Next Steps" section within the notables.

## Convert Searches to Correlation Searches

- Correlation Searches provide enhanced possibilities for investigating events.
- To transform a search, add the following parameters: [^1]

```conf
# savedsearches.conf
action.correlationsearch = 0
action.correlationsearch.enabled = 1
action.correlationsearch.label = "rule_name"
description = "description"
```

## Data Enrichment with Asset Details

- Enrich your assets with additional information such as hostnames or departments for users.
- This can be done with the Asset & Identity Framework. [^2]

## Customize your "Incident Review" Dashboard

### Change Table Attributes

- Change the "Table Attributes" to "Incident Review" in the settings:
  - `Enterprise Security -> Configure -> Incident Management -> Incident Review Settings`
  - Add your values to the "Incident Review - Table Attributes" field.

### Use Saved Filters for Faster Filtering

- Customize the default filter view to match your needs.
- Set your filters and save them as new filters for quick access.

### Add More Data to Event Details View

- To add data to a notable, extract the data from the search and add it to the notable.
- Extract the field:
  - `correlation search -> notable -> Asset Extraction`
- Add the field to "Incident Review" configuration:
  - `Enterprise Security -> Configure -> Incident Management -> Incident Review Settings`
  - Add your values to the "Incident Review - Event Attributes" field.

## References

- [Configure correlation searches](https://docs.splunk.com/Documentation/PCI/5.1.0/Install/Correlationsearches)

[^1]: [correlationsearches.conf parameter translation to savedsearches.conf](https://docs.splunk.com/Documentation/PCI/5.1.1/Install/Correlationsearches#Changes_you_have_to_make_after_upgrade)
[^2]: [Asset & Identity for Splunk Enterprise Security - Part 1: Contextualizing Systems](https://www.splunk.com/en_us/blog/security/asset-identity-for-splunk-enterprise-security-part-1-contextualizing-systems)
