---
title: "Splunk: Asset and Identity Framework"
categories: 
  - splunk
  - tools
  - Information Security
tags:
  - blue team
classes: 
  - wide
excerpt: "Learn about Splunk's Asset and Identity Framework, including merging, troubleshooting, and useful commands."
toc: true
date: 2024-11-19
---

## Merge for Assets or Identities

If you disable the merge, only the first asset found will be correlated.

```bash
# For example, the asset_lookup_by_str lookup in transforms.conf has max_matches = 1.
# So, the first host it matches in the assets_by_str collection is the only one you'll see in your search results.
```

## Show All Assets

```bash
# Option 1
| `datamodel("Identity_Management", "All_Assets")`
| rename All_Assets.* as *

# Option 2
| `assets`
```

## Troubleshooting

```bash
index=_internal sourcetype="identity_correlation:merge" source=*entity_merge.log*
```

## References

- [Splunk Bloom Filter][def]  
- [Field Summary Command Overview][def1]  
- [About Event Segmentation][def2]  
- [Event Segmentation and Searching][def4]  
- [Commands by Type][def3]  

[def]: https://docs.splunk.com/Splexicon:Bloomfilter "Bloomfilter Documentation"
[def1]: https://docs.splunk.com/Documentation/SCS/current/SearchReference/FieldsummaryCommandOverview "Fieldsummary Command Overview"
[def2]: https://docs.splunk.com/Documentation/Splunk/latest/Data/Abouteventsegmentation "About Event Segmentation"
[def3]: https://docs.splunk.com/Documentation/Splunk/latest/SearchReference/Commandsbytype "Commands by Type"
[def4]: https://docs.splunk.com/Documentation/Splunk/latest/Search/Eventsegmentationandsearching "Event Segmentation and Searching"
