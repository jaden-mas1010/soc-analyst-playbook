# Splunk Alerting Notes

These notes explain how Splunk creates alerts from saved searches, how alert conditions work, and how SOC analysts use Splunk alerts during investigations.

---

## What a Splunk Alert Is
A Splunk alert is a **saved SPL search** that runs on a schedule and triggers when certain conditions are met.

Alerts help SOC teams detect:
- Brute force attacks
- Suspicious processes
- Malware behavior
- Network anomalies
- Privilege escalation
- Log tampering

Alerts = automated detection.

---

## How Splunk Alerts Work

### 1. Create an SPL Search
Example:
