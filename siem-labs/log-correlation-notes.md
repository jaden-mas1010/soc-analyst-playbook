# Log Correlation Notes

These notes cover how SIEM tools correlate logs from different systems to identify suspicious activity.  
Correlation is one of the most important features of a SIEM because individual logs rarely tell the full story.

---

## What Correlation Means
Correlation is the process of linking multiple events from different log sources to understand a bigger pattern.

A single event might look harmless, but when combined with others, it can reveal malicious behavior.

---

## Why Correlation Matters
- Attackers rarely trigger only one log
- Most attacks involve multiple steps across different systems
- Correlation helps analysts see the full chain of activity
- It reduces noise and highlights meaningful patterns

---

## Examples of Correlated Activity

### 1. Brute Force + Successful Login
- Multiple failed logins  
- Followed by a successful login  
- From the same IP  
- In a short time window  

This often indicates **credential stuffing** or **password guessing**.

---

### 2. VPN Login + File Access + PowerShell
- User logs in from an unusual IP  
- Accesses sensitive files  
- Runs PowerShell shortly after  

Individually, these logs look normal.  
Together, they suggest **possible account compromise**.

---

### 3. Process Execution + Network Connection
- Suspicious process starts (e.g., `powershell.exe`)  
- Immediately makes an outbound connection  

This could indicate **malware beaconing**.

---

## How SIEM Performs Correlation
- Matches fields like username, IP address, hostname, process name  
- Uses time windows (e.g., 5 minutes, 10 seconds)  
- Applies rule logic to detect patterns  
- Groups related events into a single alert

---

## Key Takeaways
- Correlation turns raw logs into meaningful alerts  
- It helps detect multi‑step attacks  
- It reduces false positives  
- It gives analysts context to understand what actually happened
