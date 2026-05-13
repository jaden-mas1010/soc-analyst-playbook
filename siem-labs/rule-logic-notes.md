# SIEM Rule Logic Notes

These notes cover how SIEM detection rules work and how they decide when to trigger an alert.  
Understanding rule logic is important because it helps analysts know *why* an alert fired and whether it’s meaningful.

---

## What Rule Logic Is
Rule logic is the set of conditions a SIEM uses to decide if an event or pattern is suspicious.  
If the conditions match, the SIEM generates an alert.

Rules can be simple or complex depending on the use case.

---

## Types of SIEM Rules

### 1. **Single-Event Rules**
Triggered by one event that meets a condition.

Examples:
- Event ID 1102 → Logs cleared
- Event ID 4625 → Failed login
- Process name contains “mimikatz.exe”

These are straightforward and fire immediately.

---

### 2. **Multi-Event (Correlation) Rules**
Triggered when multiple related events occur within a time window.

Examples:
- 5 failed logins + 1 successful login (same user, same IP)
- Suspicious process + outbound network connection
- VPN login + file access + PowerShell execution

These rules detect patterns, not isolated events.

---

### 3. **Threshold Rules**
Triggered when something happens too many times in a short period.

Examples:
- 20 failed logins in 2 minutes
- 1000 outbound connections in 10 seconds
- Large data transfer volume

Useful for brute force, scanning, or exfiltration.

---

### 4. **Anomaly-Based Rules**
Triggered when behavior deviates from normal patterns.

Examples:
- User logs in from a new country
- Process runs at an unusual time
- Host sends more traffic than usual

These rely on baselines.

---

## Common Rule Conditions
Rules often check fields like:
- Username
- Hostname
- Source IP / Destination IP
- Process name
- Command line
- Event ID
- File path
- Time window

A rule fires only when all required conditions match.

---

## Example Rule Logic (Human-Friendly)

**IF**  
Event ID = 4688  
AND process name contains “miner”  
AND parent process is not a known application  
**THEN**  
Trigger alert: “Suspicious Mining Activity Detected”

This is similar to the logic used in the SIEM lab you completed.

---

## Why Rule Logic Matters
- Helps analysts understand why alerts fire  
- Reduces false positives  
- Improves detection accuracy  
- Helps tune rules for better visibility  
- Supports incident response decisions  

Good rule logic = fewer useless alerts + more meaningful detections.

---

## Key Takeaways
- Rules are built from conditions that match suspicious behavior  
- Correlation rules detect multi-step attacks  
- Threshold rules catch brute force and scanning  
- Anomaly rules detect unusual behavior  
- Understanding rule logic helps analysts investigate alerts effectively
