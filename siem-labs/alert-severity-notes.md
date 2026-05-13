# SIEM Alert Severity Notes

These notes cover how SIEM tools classify alert severity and how analysts use severity levels to prioritize their work.  
Severity helps determine what needs immediate attention and what can wait.

---

## Why Severity Matters
- SOC analysts receive a lot of alerts
- Not all alerts are equally important
- Severity helps decide what to investigate first
- It reduces noise and improves response time

Good triage = faster detection + faster containment.

---

## Common Severity Levels

### 1. **Low**
- Informational or minor anomalies
- Usually not malicious
- Examples:
  - Single failed login
  - User running a common script
  - Normal background processes

Action: Monitor, no immediate response.

---

### 2. **Medium**
- Something unusual but not clearly malicious
- Needs review to confirm
- Examples:
  - Login from a new location
  - Suspicious PowerShell command
  - Unusual file access

Action: Investigate when possible.

---

### 3. **High**
- Strong indicators of malicious activity
- Needs quick investigation
- Examples:
  - Multiple failed logins + successful login
  - Suspicious process execution (e.g., rundll32, mshta)
  - Outbound traffic to unknown IPs

Action: Investigate immediately.

---

### 4. **Critical**
- Clear signs of compromise or active attack
- Requires immediate response
- Examples:
  - Malware execution
  - Privilege escalation
  - Data exfiltration
  - Lateral movement

Action: Contain the host, escalate to IR team.

---

## How Severity Is Determined
SIEMs use:
- Rule logic
- Event type
- Number of matched conditions
- Known malicious indicators
- Threat intelligence feeds
- Behavior patterns

Analysts may adjust severity based on context.

---

## Analyst Considerations
When reviewing severity, I check:
- Is the user expected to do this?
- Is the host sensitive (server, domain controller)?
- Has this happened before?
- Is the activity spreading?

Severity is a guide, not a final answer.

---

## Key Takeaways
- Severity helps prioritize alerts
- High and critical alerts need immediate attention
- Medium alerts require context to decide
- Low alerts are usually informational
- Good triage improves SOC efficiency
