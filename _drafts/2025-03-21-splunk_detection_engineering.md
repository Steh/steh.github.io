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
    * dive into the documentation
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
2. baselining:
    * ML
        * https://docs.splunk.com/Documentation/MLApp/5.5.0/User/AboutMLTK
        * https://github.com/splunk/security_content/blob/develop/baselines/baseline_of_dns_query_length___mltk.yml
    * stats
        * 
3. Test Detections:
    * https://attack-range.readthedocs.io/en/latest/
    * https://github.com/redcanaryco/atomic-red-team
    * https://github.com/mvelazc0/PurpleSharp
    * 


## source

* [Cybersec Cafe: My SIEM-Agnostic Creative Process to Detection Engineering][def]
* [Cybersec Cafe: Engineering the SOC: Writing a Detection Rule][def1]
* [youtube: Anomaly Detection So Easy Your Grandma Can Do It. No ML degree Required Splunk .conf 2024][def2]
* [github: Anomaly Detection So Easy Your Grandma Can Do It. No ML degree Required Splunk .conf 2024][def3]
* [cyberseccafe.com: My SIEM-Agnostic Creative Process to Detection Engineering][def4]
* [cyberseccafe.com: Detection Engineering the SOC: Writing a Detection Rule][def5]

[def]: https://osintteam.blog/my-siem-agnostic-creative-process-to-detection-engineering-4e401ac60b63
[def1]: https://www.cyberseccafe.com/p/detection-engineering-the-soc-writing
[def2]: https://www.youtube.com/watch?v=iFqz9aIfGAI
[def3]: https://github.com/lameCreations/Splunk-Conf-2024-Material
[def4]: https://www.cyberseccafe.com/p/my-siem-agnostic-creative-process
[def5]; https://www.cyberseccafe.com/p/detection-engineering-the-soc-writing