# Incident Report: SSH Brute Force Detection

## Executive Summary

A custom Elastic SIEM detection identified repeated failed SSH authentication attempts against an Ubuntu host.

The activity was generated within a controlled SOC lab environment to validate detection logic and alert generation.

---

## Alert Information

| Field              | Value                         |
| ------------------ | ----------------------------- |
| Alert Name         | Linux SSH Brute Force Attempt |
| Severity           | Medium                        |
| Risk Score         | 50                            |
| MITRE ATT&CK       | T1110 - Brute Force           |
| Data Source        | auth.log                      |
| Detection Platform | Elastic SIEM                  |

---

## Investigation

Review of Kibana alerts identified multiple failed SSH login attempts against an invalid user account.

Authentication logs showed repeated failed password events originating from localhost.

No successful authentication events were observed following the failed attempts.

---

## Findings

* Multiple failed authentication attempts detected.
* No successful login activity observed.
* Activity successfully triggered the custom detection rule.
* Alert validation completed successfully.

---

## Impact Assessment

No compromise occurred.

The activity was generated as part of authorized security testing within the home SOC environment.

---

## Recommendations

* Continue monitoring authentication activity.
* Configure account lockout policies.
* Restrict SSH access to trusted hosts.
* Review authentication logs regularly.

---

## Status

Closed – Authorized Lab Activity
