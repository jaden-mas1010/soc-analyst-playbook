# Splunk Architecture Notes

These notes explain the three core components of Splunk: the Forwarder, Indexer, and Search Head.  
Understanding this architecture is essential for SOC analysts, detection engineers, and anyone using Splunk for investigations.

---

## 1. Universal Forwarder (UF)
The **Forwarder** is installed on endpoints (Windows, Linux, servers).  
Its job is simple:

- Collect logs  
- Send logs to the Indexer  
- Use minimal system resources  
- Run quietly in the background  

Forwarders do NOT store or analyze logs — they only **ship** them.

Examples of logs sent:
- Windows Event Logs  
- Linux `/var/log` files  
- Application logs  
- Web server logs  

---

## 2. Indexer
The **Indexer** is the heart of Splunk.

It:
- Receives logs from Forwarders  
- Parses the logs  
- Extracts fields  
- Indexes the data  
- Stores the data  
- Makes logs searchable  

This is where Splunk turns raw logs into searchable events.

Indexers also:
- Handle data retention  
- Compress logs  
- Manage storage tiers  

---

## 3. Search Head (SH)
The **Search Head** is the interface analysts use.

It:
- Runs SPL queries  
- Displays dashboards  
- Generates alerts  
- Creates visualizations  
- Allows investigations  

When you type a search in Splunk, the Search Head:
1. Sends the query to the Indexer  
2. Indexer returns matching events  
3. Search Head displays results  

This is exactly what you see in the TryHackMe Splunk room — the Search Head is where you run SPL searches and build dashboards.

---
[Endpoint] → Forwarder → Indexer → Search Head → Analyst

Code

- Forwarder ships logs  
- Indexer stores & processes logs  
- Search Head queries logs  
- Analyst investigates  

---

## Why This Matters for SOC Analysts
Understanding this architecture helps you:
- Know where logs come from  
- Troubleshoot missing data  
- Understand ingestion delays  
- Build better searches  
- Investigate alerts faster  

It also shows recruiters you understand **real SIEM infrastructure**, not just theory.

---

## Key Takeaways
- Forwarder = sends logs  
- Indexer = stores & processes logs  
- Search Head = searches & dashboards  
- All three work together to power Splunk investigation

## How They Work Together

