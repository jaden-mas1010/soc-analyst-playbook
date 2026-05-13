# SIEM Alerting Process Notes

These notes explain how a SIEM generates alerts, what happens after an alert fires, and how analysts interact with the alerting workflow.  
Understanding this process is essential for SOC triage and incident response.

---

## 1. Event Enters the SIEM
A log is ingested from:
- Windows (Event Viewer)
- Linux (`/var/log/...`)
- Firewalls / routers (syslog)
- Web servers (Apache access logs)

The SIEM parses and normalizes the event so it can be used by detection rules.

---

## 2. Rule Evaluation
Every incoming event is checked against active detection rules.

Examples:
- “Failed login threshold exceeded”
- “Suspicious process execution”
- “Outbound traffic to blacklisted IP”
- “Logs cleared on host”

If the event matches the rule conditions, the SIEM moves to the next step.

---

## 3. Correlation (If Required)
For multi‑event rules, the SIEM checks:
- Time windows (e.g., 5 minutes)
- Same user / same IP / same host
- Sequence of events

Example:
- 5 failed logins → 1 successful login → same IP  
This triggers a brute‑force alert.

---

## 4. Alert Generation
If all rule conditions match, the SIEM creates an alert with:
- Severity (Low / Medium / High / Critical)
- Rule name
- Matched fields
- Timestamp
- User / host involved
- Event details

This is what appears in the SOC queue.

---

## 5. Alert Enrichment
The SIEM may add:
- Threat intelligence (malicious IPs/domains)
- Geo‑location data
- Asset criticality
- User behavior baselines
- MITRE ATT&CK mapping

Enrichment helps analysts understand the alert faster.

---

## 6. Analyst Review (Triage)
The SOC analyst checks:
- What triggered the alert
- Whether the activity is expected
- Whether the user or host is sensitive
- Whether the command line or process is suspicious
- Whether the IP/domain is malicious

This is where TP vs FP is decided.

---

## 7. Response Actions
If the alert is a **True Positive**, actions may include:
- Isolating the host
- Blocking an IP or domain
- Resetting credentials
- Killing a process
- Escalating to IR team

If it’s a **False Positive**, the rule may be tuned.

---

## 8. Rule Tuning (Optional)
To reduce noise, analysts may:
- Add exclusions
- Adjust thresholds
- Add context (e.g., known admin tools)
- Improve correlation logic

Good tuning = fewer useless alerts.

---

## Key Takeaways
- Alerts are generated only when rule logic matches event data
- Correlation helps detect multi‑step attacks
- Enrichment adds context for faster triage
- Analysts decide TP vs FP
- Tuning improves SIEM accuracy and reduces noise
