# SIEM Alert Investigation

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
![SIEM Alert] <img width="918" height="663" alt="Screenshot 2026-04-02 014214" src="https://github.com/user-attachments/assets/7fdf7086-026d-4adc-b618-f6777c0b5f8d" />


### Log Analysis
![Logs] <img width="884" height="646" alt="Screenshot 2026-04-02 014330" src="https://github.com/user-attachments/assets/5f8cc5c6-7df8-4056-aa21-76b70da1ed81" />
