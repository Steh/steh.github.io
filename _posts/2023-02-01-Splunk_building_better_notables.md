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

## Notables in Splunk Enterprise Security (ES)

Notables in Splunk Enterprise Security (ES) are security-related events that require further investigation or action by security analysts. These notables are created by rules in Splunk ES that detect suspicious or anomalous behavior in the security data.

### Contributing Events

- Add a search to display the search results leading to the notables.
- Utilize the "Drill-down Search" field within the notables to view the events.

### Next Steps Instructions

- Include clear instructions within the notables to guide the next steps for analysts.
- Make use of the "Next Steps" section within the notables.

### Convert Searches to Correlation Searches

- Correlation Searches provide advanced capabilities for investigating events.
- To transform a search into a correlation search, add the following parameters: [^1]

```conf
# savedsearches.conf
action.correlationsearch = 0
action.correlationsearch.enabled = 1
action.correlationsearch.label = "rule_name"
description = "description"
```

## Data Enrichment with Asset Details

- Enhance your assets with additional information such as hostnames or departments for users.
- Utilize the Asset & Identity Framework for data enrichment. [^2]

## Customizing the "Incident Review" Dashboard

### Changing Table Attributes

- Update the settings to change the "Table Attributes" to "Incident Review":
  - Go to `Enterprise Security -> Configure -> Incident Management -> Incident Review Settings`
  - Enter your desired values in the "Incident Review - Table Attributes" field.

### Using Saved Filters for Faster Filtering

- Customize the default filter view according to your requirements.
- Set your filters and save them as new filters for quick access.

### Adding More Data to Event Details View

- To add data to a notable, extract the relevant information from the search results and include it in the notable.
- Extract the field using the following steps:
  - `Correlation Search -> Notable -> Asset Extraction`
- Add the field to the "Incident Review" configuration:
  - Go to `Enterprise Security -> Configure -> Incident Management -> Incident Review Settings`
  - Enter your values in the "Incident Review - Event Attributes" field.

## References

- [Configure correlation searches](https://docs.splunk.com/Documentation/PCI/5.1.0/Install/Correlationsearches)

[^1]: [correlationsearches.conf parameter translation to savedsearches.conf](https://docs.splunk.com/Documentation/PCI/5.1.1/Install/Correlationsearches#Changes_you_have_to_make_after_upgrade)
[^2]: [Asset & Identity for Splunk Enterprise Security - Part 1: Contextualizing Systems](https://www.splunk.com/en_us/blog/security/asset-identity-for-splunk-enterprise-security-part-1-contextualizing-systems)
