# Windows Credential Access Techniques Notes

Credential access is when an attacker steals passwords, hashes, Kerberos tickets, or authentication tokens to escalate privileges or move laterally.  
These notes cover the most common Windows credential theft techniques and how to detect them using logs, Sysmon, and SIEM searches.

---

## 1. LSASS Dumping (Most Common Technique)

### Tools:
- Mimikatz
- ProcDump
- Task Manager (manual dump)
- comsvcs.dll (MiniDump)
- Dumpert
- Pypykatz

### Indicators:
- Sysmon Event ID **10** — Process Access (lsass.exe)
- Sysmon Event ID **1** — Process Creation (procdump.exe, rundll32.exe)
- Dump files created in Temp/AppData

### Detection:
index=sysmon EventCode=10 TargetImage="lsass.exe"

Code

### Red flags:
- procdump.exe accessing LSASS
- rundll32.exe loading comsvcs.dll
- powershell.exe accessing LSASS
- lsass.dmp files in user directories

---

## 2. SAM / SYSTEM Hive Theft

Attackers steal registry hives to extract:
- NTLM hashes
- Machine account passwords
- LSA secrets

### Indicators:
- Event ID **4656** (Handle Request)
- Event ID **4663** (Object Access)
- Sysmon Event ID **1** (reg.exe, powershell.exe)

### Suspicious commands:
reg save HKLM\SAM C:\Temp\SAM
reg save HKLM\SYSTEM C:\Temp\SYSTEM

Code

### Detection:
index=windows EventCode=4663 ObjectName="SAM"

Code

---

## 3. Credential Harvesting via Browser Password Stores

Browsers store:
- Saved passwords
- Cookies
- Session tokens

### Tools:
- LaZagne
- SharpChrome
- Mimikatz DPAPI modules

### Indicators:
- Sysmon Event ID **1** (browser credential tools)
- Access to Chrome/Edge login data files

### Red flags:
- Access to:
  - Login Data
  - Cookies
  - Web Data

---

## 4. DPAPI Credential Theft

DPAPI protects:
- Browser passwords
- Wi-Fi keys
- RDP credentials

Attackers steal:
- Master keys
- User DPAPI blobs

### Indicators:
- Sysmon Event ID **1** (mimikatz.exe, SharpDPAPI)
- Access to DPAPI master key folders

### Red flags:
- DPAPI extraction from non-admin accounts

---

## 5. Pass-the-Hash (PtH)

Attackers use stolen NTLM hashes to authenticate **without knowing the password**.

### Indicators:
- Event ID **4624** LogonType=9 (NewCredentials)
- Event ID **4648** (Explicit Credential Use)
- Logons without corresponding Kerberos tickets

### Detection:
index=windows EventCode=4624 LogonType=9

Code

---

## 6. Pass-the-Ticket (PtT)

Attackers steal Kerberos tickets (TGT/TGS) to impersonate users.

### Tools:
- Rubeus
- Mimikatz
- Kekeo

### Indicators:
- Event ID **4769** (TGS Request)
- Event ID **4768** (TGT Request)
- Unusual encryption types (RC4)
- Tickets used from unexpected hosts

### Red flags:
- Kerberos tickets used outside normal workstation
- Tickets with long lifetimes

---

## 7. Kerberoasting

Attackers request service tickets for accounts with SPNs, then crack them offline.

### Indicators:
- Event ID **4769** with:
  - Encryption type = RC4
  - ServiceName != common services

### Detection:
index=windows EventCode=4769 TicketEncryptionType=0x17

Code

### Red flags:
- Multiple TGS requests in short time
- Requests from non-server hosts

---

## 8. Overpass-the-Hash (Pass-the-Key)

Attackers use NTLM hash to request Kerberos TGT.

### Indicators:
- Event ID **4768** (TGT Request)
- No corresponding password logon

### Red flags:
- TGT requests from unusual hosts

---

## 9. Credential Access via WDigest

WDigest stores passwords in **cleartext** if enabled.

### Indicators:
- Registry modification:
HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\WDigest

Code
- Sysmon Event ID **13** (Registry Value Set)

### Red flags:
- UseLogonCredential = 1

---

## Key Takeaways
- LSASS dumping is the #1 credential theft method  
- SAM/SYSTEM hive theft gives attackers NTLM hashes  
- Kerberoasting and PtT are common in domain attacks  
- Sysmon Event IDs 1, 10, 13 are critical for detection  
- Credential access almost always leads to lateral movement
