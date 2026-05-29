# Incident Report: Port Scan Detection and Analysis

## Executive Summary

On May 29, 2026, the Elastic SIEM environment generated a security alert indicating potential reconnaissance activity against the monitored Ubuntu host. The alert was triggered by a custom detection rule designed to identify repeated port scanning behavior.

The investigation confirmed that the activity was generated during a controlled security testing exercise conducted within the Home SOC Lab environment. The purpose of the exercise was to validate log ingestion, detection logic, alert generation, and analyst investigation procedures.

The detection successfully identified the reconnaissance activity and generated actionable alerts for further review.

---

# Alert Details

| Field              | Value                        |
| ------------------ | ---------------------------- |
| Alert Name         | Potential Port Scan Activity |
| Severity           | Medium                       |
| Risk Score         | 60                           |
| Detection Platform | Elastic Security             |
| Data Source        | Filebeat                     |
| ATT&CK Technique   | T1595 – Active Scanning      |
| Status             | Closed                       |

---

# Detection Logic

The detection rule monitored log events containing indicators associated with port scanning activity.

### Detection Query

```kql
message: "PORT SCAN DETECTED"
```

The rule was configured to identify repeated reconnaissance events and generate alerts for analyst review.

---

# Investigation Timeline

### Initial Detection

The Elastic SIEM generated an alert after multiple port scan events were ingested through Filebeat and indexed into Elasticsearch.

### Event Review

The analyst reviewed the associated log events in Kibana Discover and confirmed multiple reconnaissance-related entries.

Example event:

```text
PORT SCAN DETECTED from 10.0.0.25 targeting Ubuntu host
```

### Alert Validation

The generated alert was reviewed within Elastic Security. Alert metadata, timestamps, and related events were analyzed to determine the nature of the activity.

### Scope Assessment

The investigation determined:

* Activity originated from a simulated source host.
* The Ubuntu system was the intended target.
* No exploitation attempts followed the scan activity.
* No unauthorized access was observed.

---

# Findings

The investigation confirmed the following:

✅ Detection rule functioned as expected.

✅ Log ingestion pipeline successfully captured the events.

✅ Elasticsearch indexed the events correctly.

✅ Kibana generated security alerts based on the defined detection logic.

✅ Alert triage procedures successfully identified the activity.

No evidence of compromise or malicious exploitation was identified.

---

# Impact Assessment

### Confidentiality

No impact observed.

### Integrity

No impact observed.

### Availability

No impact observed.

The activity was limited to reconnaissance behavior and did not progress to exploitation or persistence.

---

# MITRE ATT&CK Mapping

| Tactic         | Technique               |
| -------------- | ----------------------- |
| Reconnaissance | T1595 – Active Scanning |

### Description

Active Scanning refers to adversaries gathering information about target systems through techniques such as port scanning and service enumeration.

---

# Analyst Assessment

The alert accurately identified reconnaissance activity and demonstrated the effectiveness of the custom detection rule.

This exercise validated the complete detection lifecycle:

1. Event Generation
2. Log Collection
3. Data Ingestion
4. Detection Engineering
5. Alert Generation
6. Alert Triage
7. Incident Documentation

The successful completion of each phase confirms that the Elastic SIEM environment is capable of detecting and investigating reconnaissance-related security events.

---

# Recommendations

To improve security monitoring and detection capabilities, the following actions are recommended:

* Deploy network-based intrusion detection systems (IDS) such as Suricata.
* Correlate port scan activity with authentication events.
* Implement automated alert notifications.
* Develop additional reconnaissance detection use cases.
* Create dashboard visualizations for reconnaissance trends.
* Integrate threat intelligence feeds for source IP enrichment.

---

# Conclusion

The Home SOC Lab successfully detected and investigated simulated reconnaissance activity using the Elastic Stack.

The exercise demonstrated practical experience in SIEM administration, detection engineering, alert triage, and incident documentation while reinforcing key Security Operations Center workflows used in enterprise environments.

**Final Status:** Closed – Authorized Security Testing Activity
