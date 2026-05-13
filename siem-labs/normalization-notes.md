# SIEM Normalization Notes

These notes cover how SIEM tools normalize logs from different systems.  
Normalization is important because every device logs information differently, and the SIEM needs a consistent format to analyze and correlate events.

---

## What Normalization Means
Normalization is the process of converting logs from different sources into a common structure.

Example:
- Windows logs use Event IDs  
- Linux logs use plain text  
- Firewalls use vendor‑specific formats  
- Web servers use access logs  

A SIEM takes all of these and maps them into standard fields.

---

## Why Normalization Matters
- Makes searching easier  
- Allows correlation between different log sources  
- Reduces confusion caused by vendor‑specific formats  
- Helps detection rules work consistently  
- Improves alert accuracy  

Without normalization, a SIEM would be a giant pile of incompatible logs.

---

## Common Normalized Fields
Most SIEMs convert logs into fields like:
- `source_ip`
- `destination_ip`
- `username`
- `hostname`
- `process_name`
- `event_type`
- `timestamp`
- `action` (allowed, denied, executed, failed)

These fields stay the same no matter where the log came from.

---

## Example of Normalization

### Raw Windows Log
### Raw Windows Log
Event ID: 4625
Account Name: chris
Logon Type: 3
Source Network Address: 10.0.0.5

Code

### Normalized Version
event_type: failed_login
username: chris
source_ip: 10.0.0.5
logon_type: network

Code

---

## Benefits for Analysts
Normalization helps analysts:
- Search faster  
- Build better detection rules  
- Compare logs from different systems  
- Understand events without knowing vendor formats  

It also reduces the learning curve for new SOC analysts.

---

## Key Takeaways
- Normalization converts messy logs into a clean, consistent structure  
- It makes correlation and detection possible  
- It improves alert quality and reduces noise  
- It’s one of the most important parts of SIEM processing
