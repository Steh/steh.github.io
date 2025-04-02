---
title: "Detection Engineering with Splunk"
categories: 
- informationsecurity
tags:
- blue team
classes: 
- wide
excerpt: "based on the Introduction to Detection Engineering with Splunk Free learning from Splunk" 
toc: true
--- 

# SOC Maturity

* Metrics
    * Mean Time to Detect (MTTD)
        * MTTD measures the average time it takes for a SOC team to detect an incident or a security breach
    * Mean Time to Investigate (MTTI)
        * MTTI is the average time from the fault detection, until an investigation is initiated
    * Mean Time to Resolution (MTTR)
        * MTTR is the metric used to evaluate the average time a SOC team takes to completely resolve an incident once it has been detected.
    * False Positive Rates (FPR) and False Negative Rates (FNR)
        * FPR, or False positive rate, measures the percentage of incidents that are incorrectly classified as cybersecurity incidents but are not actual threats.
        * False negative rate (FNR) is the percentage of incidents that are mistakenly categorized as non-cyber threats but are actually cyber threats.
# detection engineering cycle.

1. Research
    * This may include reviewing feedback from experts like threat researchers, analysts, or threat hunters to stay informed about the latest trends and vulnerabilities
2. Collect Data
    * use sample data sets or run attack simulations to generate meaningful data for analysis and use in building detections.
3. Build Detections
    * establish what type of detection you are building, such as a rule/signature or anomaly based detection. You will crafting your search to detect the threat within your raw data.
4. Test and Tune
    *  use the data you collect to test and tune your detection to reduce false positives, and align with your organization's unique security needs
5. Review
    * don't forget to regularly review and update your detections to ensure they stay effective as threats evolve. This may even involve deprecating obsolete detections.

# getting ready

1. Normalize your Data
    * convert non-standard field names into a uniform set of standardized fields
    * use Technologie Addons (TA-)
2. baselining with ml toolkit
    * https://docs.splunk.com/Documentation/MLApp/5.5.0/User/AboutMLTK
    * https://github.com/splunk/security_content/blob/develop/baselines/baseline_of_dns_query_length___mltk.yml
3. Test Detections:
    * https://attack-range.readthedocs.io/en/latest/
    * https://github.com/redcanaryco/atomic-red-team
    * https://github.com/mvelazc0/PurpleSharp
    * 


## source

* [Text][def]

[def]: https://steh.github.io
