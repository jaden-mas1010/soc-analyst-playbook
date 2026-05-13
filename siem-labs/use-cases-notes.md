# SIEM Use Cases Notes

These notes cover common SIEM use cases — the real scenarios that detection rules are built for.  
Use cases help define what suspicious behavior looks like and how the SIEM should detect it.

---

## What a Use Case Is
A use case describes:
- A type of suspicious or malicious activity
- The logs involved
- The conditions that indicate the activity
- The alert that should be generated

Use cases are the foundation of SIEM detection engineering.

---

## Common SIEM Use Cases

### 1. Brute Force Login Attempts
**Goal:** Detect repeated failed logins.  
**Logs:** Windows Event ID 4625, Linux auth.log.  
**Indicators:**
- Many failed logins in a short time
- Same username or same IP
- Followed by a successful login

---

### 2. Suspicious Process Execution
**Goal:** Detect high‑risk executables.  
**Logs:** Windows Event ID 4688.  
**Indicators:**
- rundll32, mshta, wmic, regsvr32
- PowerShell with encoded commands
- Processes running from unusual paths (Temp, AppData)

---

### 3. Privilege Escalation
**Goal:** Detect attempts to gain admin rights.  
**Logs:** Security logs, Sysmon.  
**Indicators:**
- Token manipulation
- UAC bypass attempts
- Admin group membership changes

---

### 4. Lateral Movement
**Goal:** Detect attackers moving between systems.  
**Logs:** Windows logon events, network logs.  
**Indicators:**
- Remote logins (Event ID 4624 Type 3 or 10)
- SMB connections between hosts
- Remote PowerShell or WMI usage

---

### 5. Data Exfiltration
**Goal:** Detect large or unusual outbound traffic.  
**Logs:** Firewall logs, proxy logs.  
**Indicators:**
- Large data transfers
- Traffic to unknown countries
- Uploads to cloud storage services

---

### 6. Malware Execution
**Goal:** Detect known malicious behavior.  
**Logs:** Endpoint logs, process creation logs.  
**Indicators:**
- Known malware hashes
- Suspicious child processes
- Files dropped in Temp or AppData

---

### 7. Log Tampering
**Goal:** Detect attempts to hide activity.  
**Logs:** Windows Event ID 1102.  
**Indicators:**
- Event logs cleared
- Audit policy changes
- Disabled logging services

---

### 8. USB Device Insertion
**Goal:** Detect removable media usage.  
**Logs:** Windows device logs.  
**Indicators:**
- New USB device connected
- File transfers shortly after

---

## Why Use Cases Matter
- They guide how detection rules are built
- They help SOC teams focus on real threats
- They ensure consistent monitoring across environments
- They reduce false positives by defining clear logic

---

## Key Takeaways
- Use cases describe what suspicious activity looks like
- Each use case maps to specific logs and conditions
- Good use cases improve detection quality
- They form the backbone of SIEM rule development
