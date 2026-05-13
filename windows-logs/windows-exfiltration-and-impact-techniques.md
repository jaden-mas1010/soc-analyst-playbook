# Windows Exfiltration & Impact Techniques Notes

Exfiltration and impact are the final stages of an attack.  
Exfiltration = stealing data  
Impact = damaging systems (ransomware, wiping, encryption, destruction)

These notes cover the most common Windows exfiltration and impact techniques and how to detect them using logs, Sysmon, and SIEM searches.

---

## 1. Data Staging (Preparing Data for Theft)

Attackers rarely exfiltrate raw files.  
They **stage** data first.

### Indicators:
- Large ZIP/RAR files created
- Files copied to Temp or Public folders
- Sysmon Event ID **11** (File Created)

### Suspicious commands:
tar -cf data.tar C:\Users\*
powershell Compress-Archive -Path C:\Data -DestinationPath C:\Temp\backup.zip

Code

### Detection:
index=sysmon EventCode=11 TargetFilename=".zip" OR TargetFilename=".rar"

Code

---

## 2. Data Compression & Encryption Before Exfiltration

Attackers compress data to:
- Reduce size
- Hide structure
- Prepare for exfiltration

### Tools used:
- WinRAR
- 7zip
- PowerShell Compress-Archive
- Custom binaries

### Indicators:
- Sysmon Event ID 1 (Process Creation)
- Compression tools running from unusual paths

### Red flags:
- 7z.exe in Temp/AppData
- WinRAR used on servers

---

## 3. Exfiltration Over HTTP/HTTPS

### Why attackers use it:
- Blends with normal traffic
- Hard to detect
- Works through firewalls

### Indicators:
- Sysmon Event ID **3** (Network Connection)
- Large outbound transfers
- Connections to unknown domains

### Detection:
index=sysmon EventCode=3 DestinationPort=80 OR DestinationPort=443

Code

### Red flags:
- Long, continuous outbound sessions
- Data sent to newly registered domains

---

## 4. Exfiltration Over Cloud Storage

Attackers upload data to:
- Google Drive
- Dropbox
- OneDrive
- Mega.nz

### Indicators:
- Browser processes with large uploads
- Sysmon Event ID 3 (network)
- Unusual user-agent strings

### Red flags:
- Mega.nz connections from servers
- Uploads outside business hours

---

## 5. Exfiltration Over DNS (DNS Tunneling)

### Why attackers use it:
- Bypasses firewalls
- Very stealthy

### Indicators:
- Sysmon Event ID **22** (DNS Query)
- Long or encoded DNS queries
- High-frequency DNS requests

### Detection:
index=sysmon EventCode=22 QueryName="..."

Code

### Red flags:
- Base64-like subdomains
- Thousands of DNS queries per minute

---

## 6. Exfiltration Over SMB (Internal Data Theft)

### Indicators:
- Event ID **5140** (Share Access)
- Event ID **4624** LogonType=3
- Large file transfers between hosts

### Red flags:
- Workstations accessing server C$ shares
- SMB traffic between unrelated systems

---

## 7. Ransomware Behavior (Impact Phase)

### Key behaviors:
- Mass file encryption
- Shadow copy deletion
- Service termination
- Backup destruction

### Indicators:
- Sysmon Event ID **11** (File Created with .encrypted extensions)
- Sysmon Event ID **1** (vssadmin.exe)
- Event ID **7031/7034** (Service stopped)

### Shadow copy deletion:
vssadmin delete shadows /all /quiet
wmic shadowcopy delete

Code

### Detection:
index=windows EventCode=4688 CommandLine="vssadmindelete*"

Code

---

## 8. File Wiping / Destruction

### Tools:
- cipher.exe
- sdelete.exe
- custom wipers

### Indicators:
- Sysmon Event ID **1** (Process Creation)
- Sysmon Event ID **23** (File Deleted)

### Red flags:
- cipher.exe /w used on system drives
- sdelete.exe in Temp/AppData

---

## 9. Ransom Note Creation

### Indicators:
- Sysmon Event ID **11** (File Created)
- Files named:
  - README.txt
  - HOW_TO_DECRYPT.txt
  - RECOVER_FILES.html

### Detection:
index=sysmon EventCode=11 TargetFilename="decrypt"

Code

---

## Key Takeaways
- Exfiltration often starts with **staging + compression**  
- HTTP/HTTPS and cloud storage are the most common exfiltration channels  
- DNS tunneling is stealthy but detectable with Sysmon Event ID 22  
- Ransomware behavior includes shadow copy deletion, service killing, and mass file writes  
- Sysmon Event IDs 1, 3, 11, 22, 23 are critical for detection  
