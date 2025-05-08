---
title: ""
categories: 
- informationsecurity
tags:
- blue team
classes: 
- wide
excerpt: "" 
toc: true
--- 

# Incident Handling Life Cycle
1. Preparation

The preparation phase covers the readiness of an organization against an attack. That means documenting the requirements, defining the policies, incorporating the security controls to monitor like EDR / SIEM / IDS / IPS, etc. It also includes hiring/training the staff.


2. Detection and Analysis

The detection phase covers everything related to detecting an incident and the analysis process of the incident. This phase covers getting alerts from the security controls like SIEM/EDR investigating the alert to find the root cause. This phase also covers hunting for the unknown threat within the organization.


3. Containment, Eradication, and Recovery

This phase covers the actions needed to prevent the incident from spreading and securing the network. It involves steps taken to avoid an attack from spreading into the network, isolating the infected host, clearing the network from the infection traces, and gaining control back from the attack.

4. Post-Incident Activity / Lessons Learnt

This phase includes identifying the loopholes in the organization's security posture, which led to an intrusion, and improving so that the attack does not happen next time. The steps involve identifying weaknesses that led to the attack, adding detection rules so that similar breach does not happen again, and most importantly, training the staff if required.

# Security Principles

## CIA

* Confidentiality ensures that only the intended persons or recipients can access the data.
* Integrity aims to ensure that the data cannot be altered; moreover, we can detect any alteration if it occurs.
* Availability aims to ensure that the system or service is available when needed.

## DAD
The security of a system is attacked through one of several means. It can be via the disclosure of secret data, alteration of data, or destruction of data.

* Disclosure is the opposite of confidentiality. In other words, disclosure of confidential data would be an attack on confidentiality.
* Alteration is the opposite of Integrity. For example, the integrity of a cheque is indispensable.
* Destruction/Denial is the opposite of Availability.

## Fundamental Concepts of Security Models

### Bell-LaPadula Model

The Bell-LaPadula Model is primarily concerned with maintaining the confidentiality of information. It was developed in the 1970s for military applications to enforce access controls in a manner that prevents unauthorized disclosure of information. The model is based on two main principles:

* **Simple Security Property** : This property is referred to as “no read up”; it states that a subject at a lower security level cannot read an object at a higher security level. This rule prevents access to sensitive information above the authorized level.
* **Star Security Property** : This property is referred to as “no write down”; it states that a subject at a higher security level cannot write to an object at a lower security level. This rule prevents the disclosure of sensitive information to a subject of lower security level.
* **Discretionary-Security Property** : This property uses an access matrix to allow read and write operations. An example access matrix is shown in the table below and used in conjunction with the first two properties.

### Biba Model

The Biba Integrity Model focuses on maintaining the integrity of data rather than confidentiality. It was developed to prevent information from being altered in unauthorized ways. The model introduces the following key principle

* **Simple Integrity Property** : This property is referred to as “no read down”; a higher integrity subject should not read from a lower integrity object.
* **Star Integrity Property** : This property is referred to as “no write up”; a lower integrity subject should not write to a higher integrity object.

### Clark-Wilson Model

The Clark-Wilson Model also aims to achieve integrity by using the following concepts:

* **Constrained Data Item (CDI)** : This refers to the data type whose integrity we want to preserve.
* **Unconstrained Data Item (UDI)** : This refers to all data types beyond CDI, such as user and system input.
* **Transformation Procedures (TPs)** : These procedures are programmed operations, such as read and write, and should maintain the integrity of CDIs.
* **Integrity Verification Procedures (IVPs)** : These procedures check and ensure the validity of CDIs.

## ISO/IEC 19249

1 **Least Privilege**: You can also phrase it informally as “need-to basis” or “need-to-know basis” as you answer the question, “who can access what?” The principle of least privilege teaches that you should provide the least amount of permissions for someone to carry out their task and nothing more. For example, if a user needs to be able to view a document, you should give them read rights without write rights.
2. **Attack Surface Minimisation**: Every system has vulnerabilities that an attacker might use to compromise a system. Some vulnerabilities are known, while others are yet to be discovered. These vulnerabilities represent risks that we should aim to minimize. For example, in one of the steps to harden a Linux system, we would disable any service we don’t need.
3. **Centralized Parameter Validation**: Many threats are due to the system receiving input, especially from users. Invalid inputs can be used to exploit vulnerabilities in the system, such as denial of service and remote code execution. Therefore, parameter validation is a necessary step to ensure the correct system state. Considering the number of parameters a system handles, the validation of the parameters should be centralized within one library or system.
4. **Centralized General Security Services**: As a security principle, we should aim to centralize all security services. For example, we would create a centralized server for authentication. Of course, you might take proper measures to ensure availability and prevent creating a single point of failure.
5. **Preparing for Error and Exception Handling**: Whenever we build a system, we should take into account that errors and exceptions do and will occur. For instance, in a shopping application, a customer might try to place an order for an out-of-stock item. A database might get overloaded and stop responding to a web application. This principle teaches that the systems should be designed to fail safe; for example, if a firewall crashes, it should block all traffic instead of allowing all traffic. Moreover, we should be careful that error messages don’t leak information that we consider confidential, such as dumping memory content that contains information related to other customers.


## source

* [Text][def1]

[def1]: https://tryhackme.com/room/securityprinciples
