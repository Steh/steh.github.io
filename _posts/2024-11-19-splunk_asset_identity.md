---
title: "Splunk: Asset and Identity Framework"
categories: 
- splunk
tags:
- blue team
classes: 
- wide
excerpt: ""
toc: true
--- 

# Merge for Assets or Identities

If you disable the merge only the first asset found  will be correlated.

```bash
"For example, the asset_lookup_by_str lookup in transforms.conf has max_matches = 1, so the first host it matches in the assets_by_str collection is the only one you'll see in your search results."
```

# show all assets

´´´bash
# 1
|`datamodel("Identity_Management", "All_Assets")`
| rename All_Assets.* as *

# 2
| `assets`
´´´

# Troubleshooting

```bash
index=_internal sourcetype="identity_correlation:merge" source=*entity_merge.log*
```

## source

[def]: https://docs.splunk.com/Splexicon:Bloomfilter
[def1]: https://docs.splunk.com/Documentation/SCS/current/SearchReference/FieldsummaryCommandOverview
[def2]: https://docs.splunk.com/Documentation/Splunk/latest/Data/Abouteventsegmentation
[def4]: https://docs.splunk.com/Documentation/Splunk/latest/Search/Eventsegmentationandsearching
[def3]: https://docs.splunk.com/Documentation/Splunk/latest/SearchReference/Commandsbytype