# SIEM Alert Investigations

## Summary
This repository contains multiple SIEM alert and incident response investigations performed in a SOC (Security Operations Center) lab environment. 

Each case demonstrates alert analysis, log correlation, endpoint investigation, and classification of security events as true or false positives. The projects also showcase hands-on experience with incident response workflows, including detection, investigation, and containment of threats.

---

## Cases

### Case 1: SIEM Alert Investigation
- Investigated triggered alerts
- Analyzed suspicious activity
- Correlated events across logs

### Case 2: SIEM Log Investigation
- Performed log correlation
- Identified abnormal behavior patterns
- Investigated security events

### Case 3: Incident Response (EDR Lab)
- Investigated phishing attack via email attachment
- Analyzed endpoint activity using EDR
- Identified malware execution on host
- Performed containment actions (quarantine & isolation)

---

## Case 1: Port Scanning Activity (False Positive)

## Overview

This project documents a SIEM alert investigation performed in a SOC (Security Operations Center) lab environment. The goal was to analyze a triggered alert, review log data, and determine whether the activity was malicious or expected.

## Objective

* Investigate a SIEM alert
* Analyze network log data
* Identify suspicious indicators
* Determine if the alert is a true or false positive

## Tools Used

* TryHackMe SIEM lab environment
* SIEM dashboard and logs

## Alert Summary

* Alert Type: Port Scanning Activity
* Severity: High
* Source IP: 10.0.0.8
* Destination IP: 10.0.0.3
* Time: June 12, 2024 17:24

## Investigation Process

### 1. Alert Review

The alert indicated port scanning activity originating from IP address 10.0.0.8 targeting another internal host.

### 2. Log Analysis

I reviewed the SIEM logs and observed:

* Multiple connection attempts occurring at the same time
* Traffic targeting multiple ports (e.g., 22, 53, 443)
* Repeated activity from a single source IP

These patterns are consistent with port scanning behavior.

### 3. Source Identification

By analyzing the logs, I identified the source host name as Nessus, a known vulnerability scanning tool.

### 4. Context Validation

The SOC team had prior knowledge that a vulnerability assessment was being conducted. Additionally, the Vulnerability Assessment Team had notified the SOC in advance that they would be running a spot scan. This confirmed that the activity was expected and authorized.

## Investigation Method (5 W's)

* Who: Vulnerability Assessment Team (internal) using NESSUS
* What: Port scanning activity
* When: During the scheduled testing period
* Where: Internal network (10.0.0.8 → 10.0.0.3)
* Why: Authorized vulnerability assessment (spot scan)

## Findings

* Port scanning behavior detected
* Activity originated from an internal scanning tool (Nessus)
* Multiple ports targeted in a short time frame
* Activity aligned with a planned security test
* A response was observed from the target system back to the scanning IP on port 22 (SSH)

## Outcome

* Classification: False Positive
* Reason: The activity was part of an authorized internal vulnerability scan
* Action Taken: Alert was acknowledged and closed

## Key Takeaways

* Not all alerts indicate malicious activity
* Context is critical when investigating SIEM alerts
* Recognizing legitimate tools (like Nessus) helps reduce false positives
* Proper documentation is essential in SOC workflows
* Observed responses (e.g., port 22/SSH) should be reviewed to ensure proper security configuration

## Evidence

### SIEM Alert
The screenshot below shows the SIEM alert triggered by detected port scanning activity
<img width="918" height="663" alt="case1-siem-alert" src="https://github.com/user-attachments/assets/afadf2d7-011f-47e5-bafe-06cac76561b6" />



### Log Analysis
The screenshot below shows log evidence of multiple connection attempts across different ports from the same source IP
<img width="884" height="646" alt="case1-log-analysis" src="https://github.com/user-attachments/assets/34c68a49-62dc-4a25-93db-8162f3edb5b3" />






## Case 2: CryptoMiner Activity (True Positive)

### Alert Summary
- Alert Type: Potential CryptoMiner Activity
- Severity: Medium/High
- Source: Internal host activity
- Host: HR_02
- User: chris

### Investigation Process

#### 1. Alert Review
A SIEM alert was triggered indicating potential cryptomining activity based on predefined detection rules.

#### 2. Log Analysis
Reviewing the event logs showed a suspicious process execution:
- Process Name: cudominer.exe
- File Path: C:\Users\chris\temp\cudominer.exe

#### 3. Rule Analysis
The alert was triggered based on:
- Event ID: 4688 (process creation)
- Condition: Process name contains "miner" or "crypt"

#### 4. Source Identification
- User: chris
- Host: HR_02

### Findings
- Malicious process detected: cudominer.exe
- Executed from temp directory
- Matches cryptomining behavior

### Outcome
- Classification: True Positive
- Action Taken: Host should be isolated

### Key Takeaways
- Process names are strong indicators
- SIEM rules help detect threats
- True positives require immediate action

### Evidence

### SIEM Alert 
The screenshot below shows SIEM alert triggered by cryptomining activity 
<img width="773" height="700" alt="case2-siem-alert" src="https://github.com/user-attachments/assets/def524f9-53ca-44de-9de6-feb477d4f3e4" />


### SIEM Event Logs
<img width="796" height="576" alt="case2-event-logs" src="https://github.com/user-attachments/assets/5aab59f8-1314-45de-98bd-2be8acfa77a9" />


### RULE 
The screenshot below shows why SIEM alert triggered based this rule
<img width="757" height="431" alt="case2-rule" src="https://github.com/user-attachments/assets/41ee018d-d1a6-4cc1-a510-bb84fc793e03" />


### RESPONSE
<img width="737" height="410" alt="case2-response" src="https://github.com/user-attachments/assets/7524fa9d-6959-45a9-821d-42df17db3c2a" />




