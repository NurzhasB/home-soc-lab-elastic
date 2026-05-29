# Incident Report: SSH Brute Force Detection and Investigation

## Executive Summary

On May 29, 2026, the Elastic Security platform generated an alert indicating repeated failed SSH authentication attempts against the monitored Ubuntu host. The alert was triggered by a custom detection rule designed to identify brute-force activity targeting remote access services.

The investigation confirmed multiple failed login attempts against a non-existent user account. The activity was intentionally generated within a controlled Home SOC Lab environment to validate detection capabilities, alert generation, and investigation procedures.

The detection successfully identified the attack pattern and generated actionable alerts for analyst review.

---

# Alert Details

| Field              | Value                         |
| ------------------ | ----------------------------- |
| Alert Name         | Linux SSH Brute Force Attempt |
| Severity           | Medium                        |
| Risk Score         | 50                            |
| Detection Platform | Elastic Security              |
| Data Source        | Linux auth.log                |
| ATT&CK Technique   | T1110 – Brute Force           |
| Status             | Closed                        |

---

# Detection Logic

The detection rule monitored authentication logs for repeated failed SSH login attempts.

### Detection Query

```kql id="s2n47u"
message: "Failed password"
```

The rule was configured to identify multiple authentication failures occurring within a defined time window and generate an alert for analyst investigation.

---

# Investigation Timeline

### Initial Detection

Elastic Security generated an alert after multiple failed SSH authentication events were ingested through Filebeat and indexed into Elasticsearch.

### Event Review

The analyst reviewed the related authentication events in Kibana Discover and confirmed multiple failed login attempts.

Example event:

```text id="a54jlwm"
Failed password for invalid user fakeuser from 127.0.0.1
```

### Alert Validation

The alert was reviewed within the Elastic Security interface. Event timestamps, authentication records, and associated activity were analyzed to validate the detection.

### Scope Assessment

The investigation determined:

* Multiple failed login attempts occurred.
* Authentication attempts targeted an invalid user account.
* No successful authentication events followed the failures.
* No privilege escalation activity was observed.
* No evidence of system compromise was identified.

---

# Findings

The investigation confirmed the following:

✅ Filebeat successfully collected authentication events.

✅ Elasticsearch indexed the events correctly.

✅ The custom detection rule functioned as expected.

✅ Elastic Security generated alerts based on defined thresholds.

✅ Alert triage procedures successfully identified the attack pattern.

The observed behavior is consistent with brute-force authentication attempts targeting SSH services.

---

# Impact Assessment

### Confidentiality

No impact observed.

### Integrity

No impact observed.

### Availability

No impact observed.

The activity did not result in unauthorized access or system compromise.

---

# MITRE ATT&CK Mapping

| Tactic            | Technique           |
| ----------------- | ------------------- |
| Credential Access | T1110 – Brute Force |

### Description

Brute Force techniques involve attempting multiple authentication combinations in an effort to gain unauthorized access to systems, services, or accounts.

SSH services are frequently targeted because they provide direct administrative access to Linux systems.

---

# Analyst Assessment

The detection accurately identified brute-force authentication behavior and successfully generated alerts requiring analyst review.

This exercise validated the complete security monitoring workflow:

1. Attack Simulation
2. Log Collection
3. Data Ingestion
4. Detection Engineering
5. Alert Generation
6. Alert Triage
7. Incident Documentation

The investigation confirmed that the Elastic Stack environment is capable of identifying and monitoring authentication-based attack activity.

---

# Recommendations

To improve detection and response capabilities, the following actions are recommended:

* Implement account lockout policies.
* Restrict SSH access to trusted IP addresses.
* Enforce multi-factor authentication where possible.
* Monitor authentication failures across all systems.
* Correlate brute-force activity with successful login events.
* Develop additional detections for credential access techniques.

---

# Conclusion

The Home SOC Lab successfully detected and investigated simulated SSH brute-force activity using the Elastic Stack.

The exercise demonstrated practical experience with SIEM administration, authentication monitoring, detection engineering, alert triage, and incident response documentation.

The detection logic functioned as expected and provided clear visibility into authentication-based attack behavior.

**Final Status:** Closed – Authorized Security Testing Activity

