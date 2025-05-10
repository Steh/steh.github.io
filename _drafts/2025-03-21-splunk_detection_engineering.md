---
title: "Detection Engineering with Splunk"
categories: 
- informationsecurity
tags:
- blue team
classes: 
- wide
excerpt: "Based on the Introduction to Detection Engineering with Splunk Free learning from Splunk." 
toc: true
---

## SOC Maturity

### Metrics

- **Mean Time to Detect (MTTD)**  
  Measures the average time it takes for a SOC team to detect an incident or security breach.

- **Mean Time to Investigate (MTTI)**  
  The average time from fault detection until an investigation is initiated.

- **Mean Time to Resolution (MTTR)**  
  Evaluates the average time a SOC team takes to completely resolve an incident once detected.

- **False Positive Rates (FPR) and False Negative Rates (FNR)**  
  - **FPR**: Percentage of incidents incorrectly classified as cybersecurity threats.  
  - **FNR**: Percentage of incidents mistakenly categorized as non-threats but are actual threats.

## Detection Engineering Cycle

1. **Research**  
   - Review feedback from experts like threat researchers, analysts, or hunters.  
   - Stay informed about the latest trends and vulnerabilities.  
   - Dive into relevant documentation.

2. **Collect Data**  
   - Use sample datasets or run attack simulations to generate meaningful data for analysis.

3. **Build Detections**  
   - Define the type of detection (e.g., rule/signature-based or anomaly-based).  
   - Craft searches to detect threats within raw data.

4. **Test and Tune**  
   - Use collected data to test and refine detections, reducing false positives and aligning with organizational needs.

5. **Review**  
   - Regularly review and update detections to ensure effectiveness as threats evolve.  
   - Deprecate obsolete detections when necessary.

## Getting Ready

1. **Normalize Your Data**  
   - Convert non-standard field names into standardized fields.  
   - Use Technology Add-ons (TA-).

2. **Baselining**  
   - **Machine Learning (ML)**:  
     - [Splunk Machine Learning Toolkit Documentation](https://docs.splunk.com/Documentation/MLApp/5.5.0/User/AboutMLTK)  
     - [Baseline Example: DNS Query Length](https://github.com/splunk/security_content/blob/develop/baselines/baseline_of_dns_query_length___mltk.yml)  
   - **Statistics-Based**: Use statistical methods for baselining.

3. **Test Detections**  
   - [Attack Range](https://attack-range.readthedocs.io/en/latest/)  
   - [Atomic Red Team](https://github.com/redcanaryco/atomic-red-team)  
   - [PurpleSharp](https://github.com/mvelazc0/PurpleSharp)

## Alert Triage

When triaging alerts, consider the following questions:

- What does this alert mean?  
- Was this an actual attack?  
- Was the attack successful?  
- What assets were affected?  
- What did the attacker do (or try to do)?  
- How should we respond?

## Source

- [Cybersec Cafe: My SIEM-Agnostic Creative Process to Detection Engineering][def]  
- [Cybersec Cafe: Engineering the SOC: Writing a Detection Rule][def1]  
- [YouTube: Anomaly Detection So Easy Your Grandma Can Do It. No ML Degree Required Splunk .conf 2024][def2]  
- [GitHub: Anomaly Detection So Easy Your Grandma Can Do It. No ML Degree Required Splunk .conf 2024][def3]  
- [Cybersec Cafe: My SIEM-Agnostic Creative Process to Detection Engineering][def4]  
- [Cybersec Cafe: Detection Engineering the SOC: Writing a Detection Rule][def5]

[def]: https://osintteam.blog/my-siem-agnostic-creative-process-to-detection-engineering-4e401ac60b63  
[def1]: https://www.cyberseccafe.com/p/detection-engineering-the-soc-writing  
[def2]: https://www.youtube.com/watch?v=iFqz9aIfGAI  
[def3]: https://github.com/lameCreations/Splunk-Conf-2024-Material  
[def4]: https://www.cyberseccafe.com/p/my-siem-agnostic-creative-process  
[def5]: https://www.cyberseccafe.com/p/detection-engineering-the-soc-writing