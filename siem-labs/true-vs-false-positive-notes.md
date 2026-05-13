# True Positive vs False Positive Notes

These notes cover how to distinguish between true positives and false positives in a SIEM.  
This is one of the most important skills for SOC analysts because most alerts are not actual attacks.

---

## What Is a False Positive?
A false positive is an alert that fires correctly based on rule logic, but the activity is not malicious.

Examples:
- Admin running PowerShell for maintenance
- User mistyping their password several times
- Software updating itself and spawning processes
- Backup tools generating high network traffic

False positives waste time if not handled properly, so analysts need to identify them quickly.

---

## What Is a True Positive?
A true positive is an alert that indicates real malicious or suspicious activity.

Examples:
- Multiple failed logins followed by a successful login from the same IP
- PowerShell executing encoded commands
- Rundll32 or mshta launching remote scripts
- Outbound traffic to known malicious IPs
- Malware spawning child processes

True positives require immediate investigation and action.

---

## How I Decide TP vs FP

### 1. Check the Context
- Is the user expected to do this?
- Is the host a server or a normal workstation?
- Has this happened before?

Context often decides everything.

---

### 2. Look at the Command Line
A normal command line usually means normal activity.  
Suspicious patterns include:
- Base64 strings
- Remote URLs
- Hidden/NoProfile flags
- Unusual file paths (AppData, Temp)

---

### 3. Check the Parent Process
Legitimate parent:
- explorer.exe  
- services.exe  
- trusted applications  

Suspicious parent:
- winword.exe launching PowerShell  
- mshta.exe launching scripts  
- rundll32.exe with strange arguments  

---

### 4. Check Timing and Frequency
- One failed login → normal  
- 50 failed logins in 2 minutes → suspicious  

Patterns matter more than single events.

---

### 5. Check Threat Intelligence
If the alert involves:
- Known malicious IP  
- Known malware hash  
- Known C2 domain  

It’s almost always a true positive.

---

## Examples From Real SOC Work

### False Positive Example
powershell.exe -ExecutionPolicy Bypass -File backup.ps1

Code
Backup script running daily — normal.

### True Positive Example
powershell.exe -nop -w hidden -enc <base64>

Code
Encoded command + hidden window — suspicious.

---

## Key Takeaways
- Most alerts are false positives  
- Context is the most important factor  
- Command line and parent process reveal intent  
- True positives show clear signs of malicious behavior  
- Good analysts reduce noise and focus on real threat
