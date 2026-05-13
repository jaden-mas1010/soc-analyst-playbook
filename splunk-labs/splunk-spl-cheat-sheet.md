# Splunk SPL Query Cheat Sheet

This cheat sheet contains the most useful SPL (Search Processing Language) commands for SOC analysts.  
SPL is used on the Splunk Search Head to query indexed logs and return field-value pairs.

---

## 🔍 Basic Searching

### Search all logs
index=*  

### Search specific index
index=windows  
index=linux  
index=firewall  

### Search for a keyword
index=windows "failed login"  

### Search by field
index=windows EventCode=4625  
index=linux user=root  

---

## ⏱ Time Filtering

### Last 15 minutes
index=windows earliest=-15m  

### Last 24 hours
index=windows earliest=-24h  

### Specific time range
earliest="05/10/2026:00:00:00" latest="05/10/2026:23:59:59"  

---

## 🧑‍💻 Authentication Queries

### Failed logins
index=windows EventCode=4625  

### Successful logins
index=windows EventCode=4624  

### Logins from a specific IP
index=windows EventCode=4624 src_ip="10.0.0.5"  

---

## ⚙️ Process Execution Queries

### All process creation events
index=windows EventCode=4688  

### Search for PowerShell
index=windows EventCode=4688 process_name="powershell.exe"  

### Suspicious encoded PowerShell
index=windows EventCode=4688 CommandLine="*enc*"  

---

## 📁 File Access Queries

### File access attempts
index=windows EventCode=4663  

### Search for access to sensitive files
index=windows EventCode=4663 ObjectName="*passwords*"  

---

## 🛜 Network Activity Queries

### Outbound connections
index=windows EventCode=5156  

### Search for traffic to a specific country/IP
index=firewall dest_ip="*"  

---

## 📊 Useful SPL Commands

### stats
Count, sum, avg, group by fields.

Example:
index=windows EventCode=4625  
| stats count by Account_Name  

### table
Show selected fields in a clean table.

Example:
index=windows EventCode=4624  
| table _time, Account_Name, src_ip  

### dedup
Remove duplicates.

Example:
index=windows EventCode=4624  
| dedup Account_Name  

### sort
Sort results.

Example:
| sort - _time  

### top
Show most frequent values.

Example:
index=windows EventCode=4625  
| top Account_Name  

---

## 🧠 Correlation Examples

### Brute force detection
index=windows EventCode=4625  
| stats count by Account_Name, src_ip  
| where count > 10  

### Suspicious parent-child process
index=windows EventCode=4688  
| table
