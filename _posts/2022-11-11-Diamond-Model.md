---
title: "The Diamond Model of Intrusion Analysis"
categories: 
  - informationsecurity
tags: 
  - frameworks
classes: 
  - wide
excerpt: ""
toc: true
date: 2022-11-11
---

## The Diamond Model of Intrusion Analysis

* Adversary
  * Adversary Operator
  * Adversary Customer
* Victim
  * Victim Personae
  * Victim Assets
* Infrastructure
  * Type 1 Infrastructure - infrastructure controlled or owned by the adversary
  * Type 2 Infrastructure
* Event Meta-Features
  * "The event meta-features expand the model slightly to include non-critical, but important, elements of Diamond events. The meta-features described here are those which we find most useful, but the model is not limited to these. Those who implement or extend our model may wish to add additional meta-features to capture other critical elements of information associated with an event."
  * Timestamp - Event occurred
  * Phases
  * Result - Result of adversary’s operations: Success, Failure, Unknown
  * Direction - Network or Host-based
  * Methodology - Describe the general class of activity, for example: spear-phish email, content-delivery attack, etc.
  * Resources - Resources involved like Software (metasploit), Knowledge (run metasploit), Information, Hardware, Funds, Facilities, Access
* Social-Political - Describes the needs and intent of the adversary
* Technology

## References

* [PDF: The Diamond Model of Intrusion Analysis](https://www.activeresponse.org/wp-content/uploads/2013/07/diamond.pdf)
* [TryHackMe: Diamond Model](https://tryhackme.com/room/diamondmodelrmuwwg42)
