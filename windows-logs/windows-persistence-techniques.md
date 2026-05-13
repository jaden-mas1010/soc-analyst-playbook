# Windows Persistence Techniques Notes

Persistence is how attackers maintain long-term access to a compromised Windows system.  
These notes cover the most common persistence mechanisms and how to detect them using Windows Event Logs, Sysmon, and SIEM searches.

---

## 1. Registry Run Keys

### Paths:
- HKCU\Software\Microsoft\Windows\CurrentVersion\Run
- HKLM\Software\Microsoft\Windows\CurrentVersion\Run
- HKCU\Software\Microsoft\Windows\CurrentVersion\RunOnce
- HKLM\Software\Microsoft\Windows\CurrentVersion\RunOnce

### Why attackers use it:
- Executes malware at every login
- Easy to hide
- Works for all users (HKLM)

### Detection:
- Sysmon Event ID 13 (Registry Value Set)
- Suspicious executables in AppData/Temp
- Unexpected new entries

### Splunk query:
index=windows EventCode=13 TargetObject="\\Run"

Code

---

## 2. Scheduled Tasks

### Why attackers use it:
- Executes payloads on a schedule
- Can run as SYSTEM
- Common for ransomware and backdoors

### Detection:
- Windows Event ID 4698 (Task Created)
- Sysmon Event ID 1 (Process Creation)
- Tasks running from Temp/AppData

### Suspicious example:
schtasks /create /tn "Updater" /tr C:\Users\...\Temp\payload.exe /sc minute /mo 5

Code

---

## 3. Services (Service-Based Persistence)

### Why attackers use it:
- Runs at startup
- Can run with SYSTEM privileges
- Very stealthy

### Detection:
- Windows Event ID 7045 (New Service Installed)
- Sysmon Event ID 1 (Process Creation)
- Services pointing to non-standard paths

### Splunk query:
index=windows EventCode=7045

Code

---

## 4. Startup Folder Persistence

### Paths:
- C:\Users\<user>\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup
- C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup

### Why attackers use it:
- Simple and reliable
- Executes on user login

### Detection:
- Sysmon Event ID 11 (File Created)
- Suspicious EXEs or scripts in Startup folder

---

## 5. WMI Persistence

### Why attackers use it:
- Fileless
- Hard to detect
- Used by APTs and advanced malware

### Detection:
- Sysmon Event IDs:
  - 19 (WMI Event Filter)
  - 20 (WMI Event Consumer)
  - 21 (WMI Binding)

### Splunk query:
index=sysmon EventCode IN (19,20,21)

Code

---

## 6. Registry “Image File Execution Options” (IFEO)

### Why attackers use it:
- Hijacks legitimate executables
- Executes malware instead of real program

### Path:
HKLM\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options

Code
