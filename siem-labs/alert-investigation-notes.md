# Alert Investigation Notes

These notes cover how I approach investigating alerts inside a SIEM.  
The goal is to understand what triggered the alert, whether it’s legitimate, and what action should be taken.

---

## 1. Start With the Alert Details
When an alert fires, the first thing I check is:
- The rule name
- The fields that matched the rule
- The timestamp
- The user or host involved

This gives a quick idea of what the SIEM thinks is suspicious.

---

## 2. Review the Events Behind the Alert
Most alerts are based on multiple events.  
I look at:
- Event IDs (Windows)
- Log source (Windows, Linux, firewall, web server)
- Process names
- Command lines
- IP addresses
- Parent/child processes

This helps confirm whether the activity is normal or unusual.

---

## 3. Check the Context
Context is everything in SOC work.  
I ask myself:
- Has this user done this before?
- Is the login location normal?
- Is the process expected on this machine?
- Is the command line suspicious?
- Is the network connection legitimate?

Normal activity in the wrong context becomes suspicious.

---

## 4. Determine True Positive vs False Positive
### False Positive
- Expected behavior
- Known software
- Legitimate admin activity
- Misconfigured rule

### True Positive
- Clear malicious behavior
- Suspicious process execution
- Unusual login patterns
- Known attacker tools
- Unexpected outbound traffic

---

## 5. Take Action
Depending on the result:
- Contact the user or asset owner
- Isolate the host
- Block an IP or domain
- Reset credentials
- Tune the rule if needed

The goal is to contain the threat quickly and avoid unnecessary disruption.

---

## Key Takeaways
- Alerts are starting points, not conclusions
- Always check the events behind the alert
- Context determines whether something is malicious
- Good investigation reduces noise and improves detection quality
