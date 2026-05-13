# SIEM Limitations & Challenges Notes

These notes cover the real‑world limitations and challenges of SIEM tools.  
Every SOC analyst eventually learns that SIEMs are powerful, but not perfect.

---

## 1. High Volume of Alerts
SIEMs generate a huge number of alerts.
- Many are false positives
- Some are low‑value noise
- Analysts can get overwhelmed

This is why triage and rule tuning matter.

---

## 2. False Positives
One of the biggest challenges:
- Normal admin activity triggers alerts
- Poorly written rules fire too often
- Lack of context causes unnecessary noise

Too many false positives = alert fatigue.

---

## 3. Blind Spots
SIEMs only see what is logged.
If something isn’t logged, the SIEM is blind to it.

Examples:
- Disabled logging
- Unsupported log sources
- Network segments not sending logs
- Cloud services without integration

No logs = no visibility.

---

## 4. Log Ingestion Delays
Sometimes logs arrive late due to:
- Network issues
- Forwarder problems
- High log volume
- Indexer overload

Delayed logs = delayed detection.

---

## 5. Storage & Cost
SIEMs are expensive to run:
- Storage costs increase with log volume
- Licensing often depends on data ingestion rate
- Long retention periods cost more

Organizations must balance visibility vs cost.

---

## 6. Complex Rule Tuning
Rules require constant tuning:
- Too strict → miss attacks
- Too loose → too many alerts
- Environment changes break rules
- New threats require new logic

Detection engineering is ongoing work.

---

## 7. Limited Behavioral Understanding
Traditional SIEMs struggle with:
- Subtle anomalies
- Insider threats
- Slow, low‑and‑slow attacks
- Living‑off‑the‑land techniques

This is why many SOCs add UEBA or EDR.

---

## 8. Dependency on Good Logging
If logs are:
- Misconfigured
- Missing fields
- Not normalized
- Incomplete

Then SIEM detections become unreliable.

Garbage in = garbage out.

---

## 9. Skill Requirements
