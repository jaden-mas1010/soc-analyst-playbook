# Windows Event ID Cheat Sheet

This cheat sheet lists the most important Windows Event IDs used in SOC investigations.  
These are the IDs analysts search for when investigating authentication issues, process execution, privilege escalation, and lateral movement.

---

## 🔐 Authentication Events

### 4624 — Successful Login
Indicates a successful authentication.  
Important fields: Logon Type, Account Name, Source IP.

### 4625 — Failed Login
Indicates a failed authentication attempt.  
Useful for brute force detection.

### 4648 — Logon Using Explicit Credentials
Often seen in lateral movement (Pass‑the‑Hash / Pass‑the‑Ticket).

### 4634 — Logoff
User session ended.

### 4672 — Special Privileges Assigned
Triggered when an account logs in with admin‑level privileges.

---

## 🧑‍💻 Account & User Activity

### 4720 — User Account Created
Possible malicious account creation.

### 4722 — User Account Enabled
Disabled account reactivated — suspicious if unexpected.

### 4723 / 4724 — Password Change / Reset
Useful for detecting compromised accounts.

### 4728 — User Added to Security Group
Critical for privilege escalation detection.

---

## ⚙️ Process & Execution Events

### 4688 — New Process Created
One of the most important logs for detecting malware and LOLBins.  
Check: Parent process, command line, file path.

### 4697 — Service Installed
Often used by attackers for persistence.

### 7045 — New Service Installed (System Log)
Also indicates persistence.

---

## 📁 File & Object Access

### 4663 — File Access Attempt
Useful for data exfiltration or ransomware detection.

---

## 🛜 Network & Remote Access

### 4627 — Group Membership Info
Useful for understanding user privileges.

### 4647 — User Initiated Logoff
Helps track session behavior.

### 5140 — Network Share Access
Useful for lateral movement detection.

### 5156 — Windows Filtering Platform Allowed Connection
Shows outbound/inbound network connections.

---

## 🧹 Clearing Logs (Very Suspicious)

### 1102 — Audit Log Cleared
One of the strongest indicators of malicious activity.

---

## 🛠️ Scheduled Tasks & Persistence

### 4698 — Scheduled Task Created
Common persistence technique.

### 4702 — Scheduled Task Updated
Attackers modify tasks to maintain access.

---

## 🔑 Kerberos & Ticket Abuse

### 4768 — Kerberos TGT Requested
Useful for detecting password spraying.

### 4769 — Kerberos Service Ticket Requested
Useful for detecting lateral movement.

### 4776 — NTLM Authentication
Useful for detecting NTLM brute force.

---

## Key Takeaways
- These Event IDs form the backbone of Windows investigations  
- 4624, 4625, 4688, 4672, and 1102 are the most commonly used  
- Understanding these IDs helps analysts detect brute force, malware, persistence, and lateral movement  
