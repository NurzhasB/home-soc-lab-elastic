# SSH Brute Force Investigation Runbook

## Purpose

This runbook provides a standardized investigation procedure for security analysts responding to SSH brute-force alerts within the Elastic SIEM environment.

The goal is to rapidly determine whether the activity represents a failed intrusion attempt, a successful account compromise, or authorized activity.

---

# Alert Overview

### Alert Name

Linux SSH Brute Force Attempt

### Severity

Medium

### MITRE ATT&CK

* T1110 – Brute Force

### Data Sources

* Linux auth.log
* Filebeat
* Elasticsearch
* Kibana Security

---

# Threat Description

Brute-force attacks occur when an adversary repeatedly attempts to authenticate against a service using multiple username and password combinations.

SSH services are frequently targeted because they provide direct access to Linux systems and administrative resources.

Common attacker objectives include:

* Initial Access
* Privilege Escalation
* Persistence
* Lateral Movement

---

# Investigation Workflow

## Phase 1: Alert Validation

### Objective

Determine whether the alert is legitimate and accurately triggered.

### Actions

Review:

* Alert name
* Detection rule
* Timestamp
* Affected host
* Alert frequency

Verify related events:

```kql
message: "Failed password"
```

### Expected Result

Multiple failed authentication attempts should be visible.

---

## Phase 2: Scope Identification

### Objective

Identify who was targeted and from where.

### Questions

* Which account was targeted?
* Was the account valid?
* Was a privileged account targeted?
* How many failures occurred?

Review authentication events for:

* Username
* Source host
* Time range
* Frequency

### Indicators of Increased Risk

* Administrator accounts targeted
* Multiple usernames targeted
* High-volume authentication failures

---

## Phase 3: Successful Authentication Review

### Objective

Determine whether the attacker gained access.

Review logs for successful logins occurring shortly after failures.

Look for events indicating:

* Successful authentication
* Session creation
* New user sessions

### Escalate Immediately If

* Successful login follows brute-force activity
* Root account login observed
* Privileged account access detected

---

## Phase 4: Host Impact Assessment

### Objective

Determine whether post-authentication activity occurred.

Review:

* Process execution
* Privilege escalation attempts
* New user creation
* Service modifications

Questions:

* Were administrative commands executed?
* Were new accounts created?
* Were security controls disabled?

---

## Phase 5: Analyst Assessment

Classify activity:

### False Positive

Authorized testing or expected activity.

### Suspicious Activity

Brute-force behavior observed but no compromise confirmed.

### Confirmed Security Incident

Successful authentication or evidence of unauthorized access.

---

# Containment Procedures

If compromise is suspected:

### Immediate Actions

* Block source IP address
* Disable affected account
* Force password reset
* Terminate active sessions

### Additional Actions

* Review firewall rules
* Enable enhanced monitoring
* Collect forensic evidence

---

# Escalation Criteria

Escalate to Incident Response if:

* Successful login occurs after failures
* Multiple hosts are targeted
* Administrative accounts are involved
* Lateral movement indicators are identified
* Malware activity is observed

---

# Recovery Actions

* Restore affected credentials
* Review authentication policies
* Implement account lockout controls
* Enforce MFA where possible

---

# Closure Criteria

The alert may be closed when:

* Activity is determined to be authorized.
* No successful compromise occurred.
* Investigation findings are documented.
* Recommended actions have been completed.

---

# Lessons Learned

Document:

* Detection effectiveness
* Investigation timeline
* Gaps in visibility
* Recommended detection improvements
