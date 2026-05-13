# Log Storage & Retention Notes

These notes explain how SIEMs store logs, how long logs are kept, and why retention matters for security, compliance, and investigations.

---

## Why Log Retention Matters
- Helps investigate incidents that happened weeks or months ago
- Supports compliance requirements (PCI-DSS, ISO 27001, SOC2)
- Allows long-term trend analysis
- Ensures evidence is available for forensic investigations

Without proper retention, you lose visibility into past activity.

---

## Types of Log Storage

### 1. Hot Storage
- Fast, searchable, real-time access
- Used for recent logs (hours to days)
- Supports active investigations and dashboards
- More expensive

Example: Last 7–30 days of logs.

---

### 2. Warm Storage
- Slightly slower but still searchable
- Used for medium-term retention
- Balanced cost vs performance

Example: 1–3 months of logs.

---

### 3. Cold Storage
- Cheapest storage (archive)
- Not instantly searchable — requires rehydration
- Used for long-term compliance retention

Example: 6 months to several years.

---

## Typical Retention Periods
These vary by organization, but common standards are:

- **30 days** → Hot storage  
- **90 days** → Warm storage  
- **1 year** → Cold storage  
- **7 years** → Compliance-heavy industries (finance, healthcare)

---

## Factors That Affect Retention
- Storage cost  
- Compliance requirements  
- Log volume  
- SIEM licensing model  
- Investigation needs  

More logs = more visibility, but also more cost.

---

## Log Rotation
To manage storage, SIEMs rotate logs:
- Old logs move from hot → warm → cold
- Very old logs may be deleted after retention period
- Rotation prevents storage overload

---

## Analyst Considerations
When investigating:
- Recent alerts use hot storage  
- Older incidents may require searching warm/cold storage  
- Cold storage may need rehydration before searching  

Understanding where logs live saves time during investigations.

---

## Key Takeaways
- Retention ensures logs are available for investigations and compliance  
- Hot storage = fast, expensive; cold storage = slow, cheap  
- Most organizations keep logs for 90 days to 1 year  
- Log rotation prevents storage issues and keeps SIEM performance stable
