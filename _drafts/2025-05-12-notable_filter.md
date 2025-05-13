---
title: "Splunk: Searchfilter for Findings in ES"
categories: 
- informationsecurity
tags:
- blue team
- splunk
classes: 
- wide
excerpt: "Restrict Access to Findings with search filters" 
toc: true
--- 

## Restrict searches per role

1. create new role and inherite the capability you need
    - ess_analyst_level1
    - ess_analyst_level2
2. restrict the search with one of the searches
```bash
# only for level1
(notable_visibilitiy=soc_level1 AND index=notable) OR (index::* AND index!=notable)

# only for level2
(notable_visibilitiy=soc_level2 AND index=notable) OR (index::* AND index!=notable)

# both
((notable_visibilitiy=soc_level1 OR notable_visibilitiy=soc_level2) AND index=notable) OR (index::* AND index!=notable)

```
3. add the field to your finding

## source

* [SPL search filter syntax][def]

[def]: https://docs.splunk.com/Documentation/Splunk/last/Security/Addandeditroles?ref=hk#SPL_search_filter_syntax
