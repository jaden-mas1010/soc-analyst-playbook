# Windows Lateral Movement Techniques Notes

Lateral movement is when an attacker moves from one compromised host to another to escalate privileges, access sensitive data, or reach domain controllers.  
These notes cover the most common techniques and how to detect them.

---

## 1. Remote Desktop Protocol (RDP)

### Indicators:
- Logon Type **10** (RemoteInteractive)
- Event ID **4624** with LogonType=10
- Event ID **4625** failed RDP attempts
- New RDP sessions at unusual hours

### Detection:
index=windows EventCode=4624 LogonType=10

Code

### Red flags:
- RDP from non-admin users
- RDP from foreign IPs
- RDP between servers that normally don’t communicate

---

## 2. SMB / Admin Shares (C$, ADMIN$)

### Used for:
- Copying payloads
- Executing remote commands
- Credential harvesting

### Indicators:
- Event ID **5140** (Network Share Access)
- Event ID **4624** LogonType=3 (Network)
- Sysmon Event ID **3** (Network Connection)

### Detection:
index=windows EventCode=5140 ShareName="\\\\*\\C$"

Code

### Red flags:
- Access to ADMIN$ from workstations
- Lateral movement between unrelated hosts

---

## 3. PsExec (psexec.exe / remoting tools)

### Why attackers use it:
- Remote command execution
- Runs as SYSTEM
- Common in ransomware

### Indicators:
- Event ID **7045** (New Service Installed)
- Sysmon Event ID **1** (Process Creation)
- Services named “PSEXESVC”

### Detection:
index=windows EventCode=7045 ServiceName="PSEXESVC"

Code

---

## 4. WMI (wmic.exe)

### Why attackers use it:
- Fileless execution
- Remote process creation
- Reconnaissance

### Indicators:
- Sysmon Event ID **1** (wmic.exe)
- Sysmon Event ID **10** (Process Access)
- WMI Event IDs 19, 20, 21

### Detection:
index=windows EventCode=4688 NewProcessName="wmic.exe"

Code

### Red flags:
- wmic.exe spawning powershell.exe
- WMI used by non-admin users

---

## 5. WinRM (PowerShell Remoting)

### Why attackers use it:
- Remote PowerShell sessions
- Stealthy lateral movement

### Indicators:
- Event ID **4624** LogonType=3
- PowerShell logs (4104)
- Sysmon Event ID 3 (network connections to port 5985/5986)

### Detection:
index=windows EventCode=4688 CommandLine="Enter-PSSession"

Code

---

## 6. Remote Scheduled Tasks

### Why attackers use it:
- Execute payloads remotely
- Persistence + lateral movement

### Indicators:
- Event ID **4698** (Task Created)
- Sysmon Event ID **1** (schtasks.exe)

### Detection:
index=windows EventCode=4688 NewProcessName="schtasks.exe"

Code

---

## 7. Remote Service Creation

### Why attackers use it:
- Execute malware remotely
- Gain SYSTEM privileges

### Indicators:
- Event ID **7045** (New Service Installed)
- Sysmon Event ID **1** (services.exe spawning unusual processes)

### Red flags:
- Services pointing to Temp/AppData
- Services created by non-admin accounts

---

## 8. Pass-the-Hash / Pass-the-Ticket

### Indicators:
- Event ID **4624** LogonType=9 (NewCredentials)
- Event ID **4648** (Explicit Credential Use)
- Kerberos anomalies (4768, 4769)

### Detection:
index=windows EventCode=4648

Code

### Red flags:
- Logons without corresponding network traffic
- Logons from unexpected hosts

---

## 9. Remote PowerShell (Encoded Commands)

### Indicators:
- Event ID **4104** (PowerShell Script Block Logging)
- Sysmon Event ID **1** (powershell.exe)
- Encoded commands (`-enc`)

### Detection:
index=windows EventCode=4688 CommandLine="powershellenc*"

Code
