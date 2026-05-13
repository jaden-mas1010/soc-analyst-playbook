# SIEM Pipeline Notes

These notes explain the full SIEM data pipeline — how logs move from endpoints into the SIEM, get processed, and eventually trigger alerts.  
Understanding this pipeline is essential for SOC analysts because every alert you investigate comes from this flow.

---

## 1. Log Generation
Every device in a network generates logs:
- **Windows** → Event Viewer logs with Event IDs (e.g., 4624, 4625, 4688)  
- **Linux** → Text-based logs like `/var/log/auth.log`, `/var/log/cron`, `/var/log/httpd`  
- **Web servers** → Apache access logs (requests, responses, user agents)

These examples match what you see in the TryHackMe room (Windows logs, Linux logs, Apache logs) .

---

## 2. Log Ingestion
Logs are sent to the SIEM using different methods:
- **Agent / Forwarder** → Installed on endpoints, sends logs automatically  
- **Syslog** → Common for Linux, firewalls, and servers  
- **Manual Upload** → Uploading offline logs for analysis  
- **Port Forwarding** → Devices send logs to a listening SIEM port  

These ingestion methods are exactly the ones listed in your TryHackMe content .

---

## 3. Parsing
Once logs reach the SIEM, they are parsed:
- Extracting fields (IP, username, process name, timestamp)
- Breaking raw text into structured data
- Identifying event types

Parsing makes logs searchable and usable for rules.

---

## 4. Normalization
Different systems log data differently.  
Normalization converts them into a **standard format** so rules can work consistently.

Examples:
- Windows Event ID 4625 → normalized to `failed_login`
- Apache access log → normalized to `web_request`
- Linux auth log → normalized to `authentication_event`

Normalization is mentioned in your TryHackMe page as the step after ingestion .

---

## 5. Correlation
The SIEM links multiple events together to detect patterns:
- Failed logins + successful login  
- Suspicious process + outbound connection  
- VPN login + file access + PowerShell execution  

Correlation is what turns raw logs into meaningful alerts.

---

## 6. Alerting
If rule conditions match, the SIEM generates an alert.

Examples:
- “Multiple Failed Logins”
- “Suspicious Process Execution”
- “Web Attack Attempt”
- “Logs Cleared on Host”

This matches the “Alerting Process and Analysis” section you’re about to reach in the TryHackMe room.

---

## Key Takeaways
- The SIEM pipeline transforms raw logs into actionable alerts  
- Each stage (ingestion, parsing, normalization, correlation) adds structure and context  
- Understanding the pipeline helps analysts investigate alerts more effectively  
- Better pipeline understanding = better triage and fewer false positives
