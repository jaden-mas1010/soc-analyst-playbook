# Windows Privilege Escalation Techniques Notes

Privilege escalation is when an attacker gains higher-level permissions (Admin, SYSTEM, Domain Admin).  
These notes cover the most common Windows privilege escalation techniques and how to detect them using logs, Sysmon, and SIEM searches.

---

## 1. Credential Dumping (LSASS Access)

### Tools:
- Mimikatz
- ProcDump
- Task Manager (manual dump)
- comsvcs.dll (MiniDump)

### Indicators:
- Sysmon Event ID **10** (Process Access)
- Access to lsass.exe by unusual processes
- Dump files in Temp/AppData

### Detection:
index=sysmon EventCode=10 TargetImage="lsass.exe"

Code

### Red flags:
- procdump.exe accessing LSASS
- rundll32.exe loading comsvcs.dll
- powershell.exe accessing LSASS

---

## 2. UAC Bypass

### Methods:
- Fodhelper.exe
- Event Viewer (eventvwr.exe)
- sdclt.exe
- ComputerDefaults.exe

### Indicators:
- Sysmon Event ID 1 (Process Creation)
- LOLBins spawning with elevated privileges

### Detection:
index=windows EventCode=4688 NewProcessName="fodhelper.exe"

Code

### Red flags:
- UAC bypass tools running from Temp/AppData

---

## 3. Token Manipulation (Pass-the-Token)

### Tools:
- Incognito
- Mimikatz
- Rubeus

### Indicators:
- Event ID **4624** LogonType=9 (NewCredentials)
- Event ID **4648** (Explicit Credential Use)

### Detection:
index=windows EventCode=4648

Code

### Red flags:
- Logons without corresponding network activity
- Logons from unexpected hosts

---

## 4. Exploiting Vulnerable Services

### Techniques:
- Unquoted service paths
- Weak service permissions
- DLL hijacking

### Indicators:
- Event ID **7045** (New Service Installed)
- Sysmon Event ID **7** (Image Loaded)
- Sysmon Event ID **1** (Process Creation)

### Detection:
index=windows EventCode=7045

Code

### Red flags:
- Services pointing to Temp/AppData
- Services created by non-admin users

---

## 5. Scheduled Task Abuse

### Why attackers use it:
- Run payloads with elevated privileges
- Persistence + escalation

### Indicators:
- Event ID **4698** (Task Created)
- Sysmon Event ID **1** (schtasks.exe)

### Detection:
index=windows EventCode=4698

Code

### Red flags:
- Tasks running EXEs from user directories
- Tasks created by unexpected accounts

---

## 6. DLL Hijacking

### Why attackers use it:
- Replace DLLs loaded by trusted apps
- Gain elevated privileges silently

### Indicators:
- Sysmon Event ID **7** (Image Loaded)
- DLLs loaded from suspicious paths

### Red flags:
- DLLs in Temp/AppData
- DLLs with random names

---

## 7. Insecure Registry Permissions

### Why attackers use it:
- Modify service configurations
- Change startup behavior
- Gain elevated execution

### Indicators:
- Sysmon Event ID **13** (Registry Value Set)

### Detection:
index=sysmon EventCode=13 TargetObject="Services"

Code

---

## 8. Named Pipe Impersonation

### Tools:
- JuicyPotato
- RoguePotato
- PrintSpoofer

### Indicators:
- Sysmon Event ID **1** (Process Creation)
- Unexpected SYSTEM-level processes

### Red flags:
- JuicyPotato.exe
- PrintSpoofer.exe
- Odd COM object activity

---

## 9. Abuse of Built‑In Admin Tools

### Tools:
- runas.exe
- at.exe
- sc.exe
- net.exe

### Indicators:
- Sysmon Event ID 1 (Process Creation)
- Event ID 4648 (Explicit Credential Use)

### Detection:
index=windows EventCode=4688 NewProcessName="runas.exe"

Code
