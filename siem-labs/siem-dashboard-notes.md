# SIEM Dashboard Notes

These notes cover how SIEM dashboards are used in day‑to‑day SOC work.  
Dashboards give analysts a quick view of what’s happening across the environment without digging into raw logs.

---

## Purpose of Dashboards
Dashboards exist to:
- Highlight unusual activity
- Show trends over time
- Surface alerts that need attention
- Provide visibility into different log sources
- Help analysts spot patterns quickly

They act as the “homepage” of a SOC analyst’s workflow.

---

## Common Dashboard Components

### 1. Authentication Activity
Shows:
- Successful logins
- Failed logins
- Login locations
- Login spikes

Useful for spotting brute‑force attempts or unusual access.

---

### 2. Process Execution
Shows:
- New processes created
- Suspicious executables
- Parent/child process relationships

Helps detect malware, LOLBins, and post‑exploitation activity.

---

### 3. Network Traffic
Shows:
- Outbound connections
- Unusual ports
- Large data transfers
- Traffic to unknown countries

Useful for spotting command‑and‑control or data exfiltration.

---

### 4. Alerts Overview
Shows:
- Total alerts
- Severity breakdown
- Alerts by category (malware, authentication, network, etc.)
- Alerts per host or user

This helps analysts prioritize what to investigate first.

---

### 5. Endpoint Activity
Shows:
- USB insertions
- File modifications
- Script execution
- Security tool events

Useful for detecting insider threats or policy violations.

---

## Why Dashboards Matter
- They reduce investigation time
- They help analysts notice patterns they might miss in raw logs
- They provide a quick health check of the environment
- They help identify spikes or anomalies instantly

---

## Key Takeaways
- Dashboards are not for deep investigation — they are for visibility
- They help analysts decide where to focus their attention
- Good dashboards reduce noise and highlight what matters
