# Port Scan Investigation Runbook

## Purpose

This runbook provides a structured methodology for investigating reconnaissance activity identified by the Elastic Security platform.

The objective is to determine whether scanning activity represents benign testing, unauthorized reconnaissance, or the early stages of an intrusion attempt.

---

# Alert Overview

### Alert Name

Potential Port Scan Activity

### Severity

Medium

### MITRE ATT&CK

* T1595 – Active Scanning

### Data Sources

* Syslog
* Filebeat
* Elasticsearch
* Kibana Security

---

# Threat Description

Port scanning is a reconnaissance technique used to identify exposed services, operating systems, and potential attack surfaces.

Adversaries frequently perform scanning before attempting exploitation.

Common objectives include:

* Service Discovery
* Vulnerability Identification
* Attack Surface Mapping
* Target Selection

---

# Investigation Workflow

## Phase 1: Alert Validation

### Objective

Confirm the legitimacy of the alert.

Review:

* Alert details
* Detection rule
* Event timestamps
* Number of triggering events

Query:

```kql
message: "PORT SCAN DETECTED"
```

### Expected Result

Multiple reconnaissance-related events should be visible.

---

## Phase 2: Source Identification

### Objective

Identify the origin of scanning activity.

Determine:

* Source IP address
* Source host
* Time range
* Scan frequency

Questions:

* Is the source internal or external?
* Is the source known?
* Has this source generated previous alerts?

---

## Phase 3: Target Assessment

### Objective

Determine what systems were targeted.

Review:

* Hostnames
* Services
* Network segments

Assess:

* Number of affected systems
* Criticality of targets
* Exposure level

---

## Phase 4: Correlation Analysis

### Objective

Identify related security events.

Review:

* Authentication alerts
* Failed login attempts
* New user activity
* Privilege escalation alerts

Questions:

* Did scanning precede authentication attempts?
* Was exploitation attempted afterward?
* Is the activity part of a larger attack chain?

---

## Phase 5: Threat Assessment

Classify the activity.

### Informational

Authorized scanning or testing activity.

### Suspicious

Unauthorized reconnaissance observed.

### High Risk

Reconnaissance followed by exploitation attempts.

---

# Containment Procedures

If unauthorized reconnaissance is confirmed:

### Immediate Actions

* Block source IP address
* Restrict network access
* Increase monitoring

### Additional Actions

* Review exposed services
* Patch vulnerable systems
* Validate firewall configurations

---

# Escalation Criteria

Escalate if:

* Critical assets are targeted
* Scanning is persistent
* Multiple hosts are affected
* Exploitation activity follows scanning
* Threat intelligence identifies the source as malicious

---

# Recovery Actions

* Harden exposed services
* Review access controls
* Validate segmentation controls
* Update monitoring coverage

---

# Closure Criteria

The alert may be closed when:

* Activity is determined to be authorized.
* No exploitation occurred.
* Findings are documented.
* Remediation actions are completed.

---

# Lessons Learned

Document:

* Detection performance
* Investigation observations
* Visibility gaps
* Monitoring improvements
* Future detection opportunities
