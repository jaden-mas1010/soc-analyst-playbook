# SIEM Notes

These are my notes from working with SIEM tools and completing hands‑on labs.  
The focus is on understanding how logs are collected, normalized, correlated, and turned into alerts.

## What SIEM Does
- Collects logs from different systems (Windows, Linux, firewalls, web servers)
- Normalizes them into a consistent format
- Correlates events to spot suspicious patterns
- Triggers alerts based on rule logic
- Provides dashboards for monitoring and investigation

## Log Sources I Worked With
### Windows
- Uses Event Viewer
- Important Event IDs:
  - 4688 – Process creation
  - 4624 – Successful login
  - 4625 – Failed login
  - 1102 – Logs cleared

### Linux
- `/var/log/auth.log` – Authentication
- `/var/log/cron` – Cron jobs
- `/var/log/httpd` – Web server logs

### Web Servers
- Apache access logs (requests, responses, user agents)

## Detection Rules
Examples of rule logic:
- Multiple failed logins in a short time
- Successful login after several failures
- USB insertion
- Outbound traffic above a threshold
- Event ID 104 → Event logs cleared
- Event ID 4688 + suspicious process name

## Alert Investigation Workflow
1. Review the event details  
2. Check which rule conditions were matched  
3. Decide if it’s a true or false positive  
4. Take action (contact user, isolate host, block IP, tune rule)

## Key Takeaways
- Normalization makes logs easier to analyze
- Correlation is what reveals the real story
- Event IDs are crucial for understanding activity
- Dashboards help spot trends quickly
- Alerts are only the starting point — investigation matters more
