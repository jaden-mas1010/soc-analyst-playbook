# Splunk Dashboard Notes

These notes explain how dashboards work in Splunk, how they are built, and how SOC analysts use them for monitoring and investigations.

---

## What a Dashboard Is
A Splunk dashboard is a collection of visual panels created from saved SPL searches.  
Dashboards help analysts monitor trends, detect anomalies, and visualize log data.

Dashboards can include:
- Tables
- Pie charts
- Bar charts
- Column charts
- Line graphs
- Single‑value indicators

Splunk supports all of these visualizations through the Search Head interface.  

---

## How Dashboards Are Built

### 1. Write an SPL Search
Every dashboard panel starts with a search.

Example:
