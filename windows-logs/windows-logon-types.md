# Windows Logon Types Cheat Sheet

Windows uses different logon types to describe *how* a user authenticated.  
Understanding these is essential for detecting brute force, RDP attacks, lateral movement, and privilege escalation.

---

## 🔐 Logon Type 2 — Interactive (Local Login)
User logged in **physically** at the machine.

Examples:
- User typing password at keyboard
- Local workstation login

SOC Use:
- Good baseline indicator
- Rarely malicious unless at odd hours

---

## 🌐 Logon Type 3 — Network Login
User accessed a resource **over the network**.

Examples:
- SMB share access
- File server access
- Lateral movement attempts

SOC Use:
- Very important for detecting lateral movement

---

## 🖥️ Logon Type 4 — Batch
Used for **scheduled tasks**.

Examples:
- Task Scheduler jobs
- Automated scripts

SOC Use:
- Unexpected batch logons may indicate persistence

---

## ⚙️ Logon Type 5 — Service
Used when a **service account** logs in.

Examples:
- Windows services starting
- Background processes

SOC Use:
- Unexpected service logons = possible persistence

---

## 🖥️➡️🖥️ Logon Type 7 — Unlock
User unlocked the workstation.

SOC Use:
- Helps track user presence

---

## 🖥️ Remote Desktop Logons

### Logon Type 10 — Remote Interactive (RDP)
User logged in via **Remote Desktop Protocol**.

SOC Use:
- Critical for detecting RDP brute force
- Key indicator of lateral movement

---

## 🛜 Logon Type 8 — NetworkCleartext
User authenticated with **cleartext credentials**.

SOC Use:
- Very suspicious
- Indicates insecure authentication or credential theft

---

## 🧪 Logon Type 9 — NewCredentials
Used with **RunAs**.

SOC Use:
- Useful for detecting privilege escalation

---

## 🛠️ Logon Type 11 — CachedInteractive
User logged in using **cached credentials**.

SOC Use:
- Common on laptops
- Useful for offline login investigations

---

## 🧠 Key Takeaways
- Logon Type **10** = RDP  
- Logon Type **3** = Network (lateral movement)  
- Logon Type **2** = Local login  
- Logon Type **5** = Service (persistence)  
- Logon Type **4** = Scheduled tasks  
- Logon Type **8** = Cleartext (dangerous)  
