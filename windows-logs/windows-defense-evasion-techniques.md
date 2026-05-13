# Windows Defense Evasion Techniques Notes

Defense evasion refers to techniques attackers use to avoid detection, disable security tools, hide activity, and blend into normal system behaviour.  
These notes cover the most common Windows defense evasion methods and how to detect them using logs, Sysmon, and SIEM searches.

---

## 1. Clearing Windows Event Logs

### Why attackers do it:
- Hide authentication failures
- Hide process execution
- Remove traces of lateral movement

### Indicators:
- Event ID **1102** — Audit Log Cleared
- Event ID **104** — Security log cleared
- Sysmon Event ID **1** (wevtutil.exe)

### Detection:
index=windows EventCode=1102

Code

### Red flags:
- wevtutil.exe run by non-admin users
- Log clearing shortly after suspicious activity

---

## 2. Disabling Security Tools

### Tools targeted:
- Windows Defender
- EDR agents
- Antivirus services
- Firewall rules

### Indicators:
- Event ID **7030/7031/7034** (Service stopped)
- Sysmon Event ID **1** (powershell.exe modifying Defender)
- Registry changes disabling AV

### Suspicious commands:
Set-MpPreference -DisableRealtimeMonitoring $true
sc stop WinDefend

Code

### Detection:
index=windows EventCode=4688 CommandLine="DisableRealtimeMonitoring"

Code

---

## 3. Timestomping (Modifying File Timestamps)

### Why attackers do it:
- Make malware look older
- Blend into legitimate system files

### Indicators:
- Sysmon Event ID **2** (File creation time changed)
- Files with timestamps older than OS install date

### Detection:
index=sysmon EventCode=2

Code

---

## 4. Obfuscated or Encoded Commands

### Common obfuscation:
- Base64 encoded PowerShell (`-enc`)
- String concatenation
- Reversed strings
- XOR‑encoded payloads

### Indicators:
- Sysmon Event ID **1** (Process Creation)
- PowerShell Event ID **4104** (Script Block Logging)

### Detection:
index=windows EventCode=4688 CommandLine="enc"

Code

### Red flags:
- Long Base64 strings
- PowerShell with no spaces
- Random variable names

---

## 5. AMSI Bypass (Anti‑Malware Scan Interface)

### Why attackers do it:
- Disable PowerShell scanning
- Run malicious scripts undetected

### Indicators:
- PowerShell Event ID **4104**
- Sysmon Event ID **1** (powershell.exe)
- Suspicious reflection or patching commands

### Suspicious example:
[Ref].Assembly.GetType("System.Management.Automation.AmsiUtils")...

Code

---

## 6. Masquerading (Fake File Names / Paths)

### Techniques:
- Malware named “svchost.exe”
- Files placed in System32 but not signed
- Fake Microsoft services

### Indicators:
- Sysmon Event ID **1** (Process Creation)
- Sysmon Event ID **7** (Image Loaded)
- Unsigned binaries in system directories

### Red flags:
- System32 files without Microsoft signatures
- Misspelled names (scvhost.exe)

---

## 7. Living‑Off‑The‑Land (LOLBins)

### Why attackers use them:
- Blend into normal activity
- Avoid detection by AV/EDR
- Execute payloads without dropping files

### Common LOLBins:
- powershell.exe
- wmic.exe
- mshta.exe
- rundll32.exe
- regsvr32.exe
- certutil.exe

### Detection:
Use Sysmon Event ID **1** + command-line analysis.

---

## 8. Uninstalling or Tampering with EDR

### Techniques:
- Killing EDR processes
- Removing drivers
- Uninstalling agents

### Indicators:
- Event ID **7031/7034** (Service crashed/stopped)
- Sysmon Event ID **1** (sc.exe, taskkill.exe)
- Missing EDR heartbeat logs

### Detection:
index=windows EventCode=4688 CommandLine="taskkill /F*"

Code
