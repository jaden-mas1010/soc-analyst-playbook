# Log Ingestion Notes

These are my notes on how SIEM tools ingest logs from different systems.  
Understanding ingestion is important because it affects visibility, detection quality, and how alerts are generated.

---

## Common Log Ingestion Methods

### 1. Agent / Forwarder
A lightweight tool installed on endpoints (Windows, Linux, servers).  
It collects important logs and sends them to the SIEM.  
Example: Splunk Forwarder.

### 2. Syslog
A standard protocol used by many devices (firewalls, routers, web servers).  
It sends real‑time logs to a central SIEM server.

### 3. Manual Upload
Some SIEMs allow uploading offline log files for quick analysis.  
Useful for investigations or one‑off log reviews.

### 4. Port Forwarding
The SIEM listens on a specific port, and devices forward logs directly to that port.

---

## Why Ingestion Matters
- Determines how fast logs reach the SIEM  
- Affects completeness of data  
- Impacts correlation and alert accuracy  
- Helps analysts understand where each log came from

---

## Key Takeaways
- Different systems use different ingestion methods  
- Agents give the most detailed logs  
- Syslog is common for network devices  
- Normalization happens after ingestion  
- Good ingestion = better detections
