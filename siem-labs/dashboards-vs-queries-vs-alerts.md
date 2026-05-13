# Dashboards vs Queries vs Alerts Notes

These notes explain the difference between dashboards, queries, and alerts in a SIEM.  
Understanding these three components is essential for SOC analysts because each one serves a different purpose in monitoring and investigation.

---

## 1. Queries (Searches)

Queries are manual searches performed by analysts to find specific logs or patterns.

### What queries are used for:
- Investigating alerts
- Searching for specific Event IDs
- Looking up user or host activity
- Filtering logs by time, IP, process, or keyword
- Building visualizations and dashboards

In Splunk, queries are written using **SPL (Search Processing Language)**, which is used to search indexed logs and return field‑value pairs .

### Examples:
- Search for failed logins  
- Search for PowerShell executions  
- Search for traffic to a specific IP  

Queries = **manual investigation tool**.

---

## 2. Dashboards

Dashboards are visual summaries built from saved queries.

### What dashboards show:
- Authentication trends  
- Process execution activity  
- Network traffic patterns  
- Alert volumes  
- Geographic login maps  
- Endpoint activity  

Dashboards help analysts **monitor the environment at a glance**.

In Splunk, dashboards are created by transforming search results into tables, pie charts, bar charts, and other visualizations .

### Dashboards are used for:
- Daily monitoring  
- Spotting anomalies  
- SOC overview  
- Reporting to management  

Dashboards = **visual monitoring tool**.

---

## 3. Alerts

Alerts are automated notifications triggered when rule conditions match incoming logs.

### Alerts are used for:
- Detecting brute force attacks  
- Detecting suspicious processes  
- Detecting malware behavior  
- Detecting unusual network activity  
- Detecting log tampering  

Alerts are generated automatically when the SIEM evaluates logs against detection rules.

### Alerts include:
- Severity  
- Rule name  
- Matched fields  
- Timestamp  
- User/host involved  

Alerts = **automated detection tool**.

---

## Summary Table

| Feature | Queries | Dashboards | Alerts |
|--------|---------|------------|--------|
| Purpose | Manual investigation | Visual monitoring | Automated detection |
| Triggered by | Analyst | Saved searches | Rule logic |
| Output | Raw logs, tables | Charts, graphs | Alert notifications |
| Used for | Deep investigation | Trend analysis | Triage & response |
| Frequency | On demand | Continuous | Real‑time |

---

## Key Takeaways
- **Queries** help analysts investigate and search logs  
- **Dashboards** help analysts monitor trends visually  
- **Alerts** notify analysts of suspicious activity automatically  
- All three work together to support SOC operations
