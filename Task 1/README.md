# Cybersecurity Log Analysis – Deloitte Forage Virtual Job Simulation

## Overview

This project contains the analysis performed for the Deloitte Cybersecurity Virtual Job Simulation on Forage. The scenario involved investigating a suspected internal breach at a fictional client, Daikibo Industrials, by analyzing real server logs. The goal was to determine whether the suspicious activity originated from outside the network or through internal VPN access.

## Files

- `analyse.ipynb`: Jupyter notebook containing all code and analysis steps.
- `web_activity.log`: The raw server log file analyzed.
- `how-to-read-the-logs.pdf`: (Optional) Guide to understanding the log format.

## What Was Done

- **Log Parsing:** The notebook parses the log file, grouping entries by IP and authorized user ID.
- **Internal vs. External IPs:** Uses regex to differentiate internal (private) and external IP addresses.
- **Suspicious Activity Detection:**
  - Checks for high-frequency API polling (potential automation/bot activity).
  - Flags user IDs with unusually high request counts.
  - Looks for user IDs used from multiple IPs (potential credential sharing/hijacking).
  - Detects regular interval API requests (automation).
  - Analyzes for brute-force login attempts.
- **Summary & Risk Assessment:** Provides a clear summary of findings and risk level.

## Key Findings

- **No evidence of external breach:** All activity originated from internal/private IPs (192.168.x.x range).
- **Suspicious internal activity:** One user ID made 122 API requests (much higher than others), with patterns suggesting automation or a compromised account.
- **No significant brute-force login attempts** were detected.

**Conclusion:**  
No external breach was found. The suspicious activity came from an internal VPN user, possibly automated or compromised.

## How to Run the Analysis

1. **Requirements:**  
   - Python 3.6+
   - Jupyter Notebook
   - Standard libraries: `re`, `datetime`, `collections` (all included in Python)

2. **Steps:**
   - Open `analyse.ipynb` in Jupyter Notebook.
   - Ensure `web_activity.log` is in the same directory.
   - Run all cells to reproduce the analysis and see the findings.

3. **Log File Format:**  
   Each block in `web_activity.log` starts with an IP address, followed by lines with:
   ```
   TIME                     METHOD REQUEST                                         STATUS
   2021-06-25T07:23:00.000Z GET    "/api/..." {authorizedUserId: "..."}           200 (SUCCESS)
   ```
   - `IP`: Source IP address
   - `TIME`: Timestamp (ISO format)
   - `METHOD`: HTTP method (GET/POST)
   - `REQUEST`: Endpoint accessed
   - `STATUS`: HTTP status and, if present, authorized user ID

## Learning Outcomes

This simulation provided practical insight into how cybersecurity teams investigate incidents using real data, including:
- Recognizing automation and abnormal usage patterns
- Differentiating internal vs. external threats
- Using Python for log analysis and incident response 