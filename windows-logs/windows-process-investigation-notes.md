# Windows Process Investigation Notes

These notes explain how to investigate Windows processes using Event Logs, Sysmon, and SIEM searches.  
Process analysis is one of the most important SOC skills for detecting malware, LOLBins, and lateral movement.

---

## 1. Key Logs for Process Investigation

### Windows Event Logs
- **4688 — New Process Created**
- **4689 — Process Terminated**

### Sysmon Logs
- **Event ID 1 — Process Creation**
- **Event ID 5 — Process Terminated**
- **Event ID 10 — Process Access**

Sysmon gives deeper visibility (hashes, command line, parent process).

---

## 2. What to Look For in a Process Event

### 🔹 Parent Process
Legitimate parent-child chains:
- explorer.exe → cmd.exe  
- services.exe → svchost.exe  
- winlogon.exe → userinit.exe  

Suspicious parent-child chains:
- winword.exe → powershell.exe  
- excel.exe → cmd.exe  
- outlook.exe → wscript.exe  
- any → rundll32.exe with weird arguments  

### 🔹 Command Line
Red flags:
- Encoded PowerShell (`-enc`)
- Base64 strings
- Long obfuscated commands
- Download commands (`Invoke-WebRequest`, `curl`, `bitsadmin`)
- Execution from Temp/AppData

### 🔹 File Path
Suspicious paths:
- `C:\Users\<user>\AppData\Local\Temp\`
- `C:\Users\<user>\AppData\Roaming\`
- `C:\ProgramData\`
- `C:\Windows\Temp\`

Legitimate programs rarely run from these folders.

### 🔹 Hashes
Check:
- VirusTotal
- Hybrid Analysis
- Any known malware signatures

---

## 3. Common LOLBins (Living-Off-The-Land Binaries)

Attackers use built‑in Windows tools to avoid detection.

### 🔥 High‑Risk LOLBins
- **powershell.exe** — execution, download, payloads  
- **cmd.exe** — script execution  
- **wmic.exe** — remote execution  
- **mshta.exe** — runs malicious HTML/JS  
- **rundll32.exe** — executes DLL payloads  
- **regsvr32.exe** — executes scripts via COM  
- **certutil.exe** — download + decode malware  
- **bitsadmin.exe** — background downloader  

If these appear with suspicious arguments → investigate immediately.

---

## 4. Suspicious Process Patterns

### 🔥 1. Office → Script → PowerShell
`winword.exe → wscript.exe → powershell.exe`  
Classic phishing → macro → payload chain.

### 🔥 2. LOLBins Running from Temp
`powershell.exe -File C:\Users\...\Temp\script.ps1`  
Malware loves Temp folders.

### 🔥 3. Rundll32 with Strange Arguments
`rundll32.exe javascript:"\..\mshtml,RunHTMLApplication"`  
Used for file
