# Sysmon Event ID Cheat Sheet

Sysmon (System Monitor) provides high‑fidelity logs that help detect malware, persistence, lateral movement, and LOLBins.  
These are the most important Sysmon Event IDs for SOC analysts.

---

## ⚙️ Process Creation

### Event ID 1 — Process Creation
The most important Sysmon event.
Shows:
- Parent process
- Command line
- Hashes
- Integrity level
- User

Used for:
- Malware detection
- LOLBins
- PowerShell abuse
- Reconnaissance

---

## 🔗 Process Relationships

### Event ID 5 — Process Terminated
Shows when a process ends.

### Event ID 7 — Image Loaded
Detects DLL injection and malicious DLL loading.

---

## 🧵 Thread Injection

### Event ID 8 — CreateRemoteThread
Used for:
- Process injection
- Malware loading code into another process

Highly suspicious.

---

## 📁 File Monitoring

### Event ID 11 — File Created
Detects:
- Malware dropping files
- Persistence files
- Suspicious executables in Temp/AppData

---

## 🔐 Registry Monitoring

### Event ID 12 — Registry Object Created/Deleted  
### Event ID 13 — Registry Value Set  
### Event ID 14 — Registry Key Renamed  

Used for detecting:
- Persistence (Run keys)
- Malware configuration changes
- Credential theft tools

---

## 🛜 Network Connections

### Event ID 3 — Network Connection
Shows:
- Source IP
- Destination IP
- Port
- Process making the connection

Used for:
- C2 detection
- Malware beaconing
- Data exfiltration

---

## 🧩 WMI Activity

### Event ID 19 — WMI Event Filter  
### Event ID 20 — WMI Event Consumer  
### Event ID 21 — WMI Event Binding  

Used for detecting:
- WMI persistence
- Fileless malware
- Lateral movement

---

## 🧪 Driver & Image Tampering

### Event ID 6 — Driver Loaded
Detects:
- Kernel‑level rootkits
- Malicious drivers

### Event ID 10 — Process Access
Used for:
- Credential dumping (LSASS access)
- Mimikatz detection

---

## 🧠 DNS Monitoring

### Event ID 22 — DNS Query
Shows:
- Domain queried
- Process making the query

Used for:
- Malware C2 domains
- Suspicious DNS tunneling
- Phishing callbacks

---

## 🧹 File Deletion

### Event ID 23 — File Deleted
Useful for:
- Malware cleanup behavior
- Anti‑forensic activity

---

## 🧠 Key Takeaways
- Sysmon provides deeper visibility than standard Windows logs  
- Event ID **1**, **3**, **10**, **11**, and **22** are the most critical  
- Sysmon is essential for detecting malware, LOLBins, and lateral movement  
- Every SOC analyst should know these IDs by heart  
