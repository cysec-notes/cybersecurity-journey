![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Platform](https://img.shields.io/badge/Platform-Kali%20Linux-blue)
![Difficulty](https://img.shields.io/badge/Difficulty-Beginner-success)
![Focus](https://img.shields.io/badge/Focus-Blue%20Team-orange)

---
# SOC Lab 1 – Investigating Linux Authentication Logs

## Overview
This hands-on lab demonstrates the fundamentals of Linux authentication log analysis from a Security Operations Center (SOC) perspective. Before learning Security Information and Event Management tools, I familiarized myself first with some concepts and fundamentals of log management, types, format, collection, storage, etc. to prepare for this lab. I understand first what is logs, how it works, where it stores, and how to analyze using Linux commands. 

Using Kali Linux with `systemd-journald`, I generated authentication events and investigated them using native Linux commands

---
## <span style="color:rgb(255, 192, 0)">Objectives:</span>
- Explain what a log is.
- Locate Linux authentication logs.
- Generate authentication events.
- Read log entries.
- Identify successful logins.
- Identify failed logins.
- Search logs using Linux commands.
- Count repeated events.
- Decide whether activity is normal or suspicious.
- Write a short investigation report.

---

### <span style="color:rgb(255, 192, 0)">Story (Real-World Scenario | 3rd person POV)</span>

You are a Tier 1 SOC Analyst at a company. At 11:00 AM, the Security Operations Center receives this alert: 

<span style="color:rgb(255, 0, 0)">"Multiple authentication events were detected on the Linux server overnight."</span>

Your team lead asks:

<span style="color:rgb(0, 176, 240)">"Determine whether these authentication events are normal user activity or something suspicious."</span>

You have access only to the Linux server. Your job is to investigate using system logs.

---

## Environment

| Component | Value |
|-----------|-------|
| Operating System | Kali Linux |
| Logging Service | systemd-journald |
| Log Source | System Journal |
| Investigation Tools | journalctl, grep, awk, sort, uniq |

---

## Authentication Events Generated

To produce realistic log data, I intentionally generated:

- Failed local login attempts
- Failed SSH login attempts
- Successful SSH logins
- Successful sudo authentication
- Failed sudo authentication

These events were later investigated using Linux log analysis techniques.

You can see how I generate authentication events ( as attacker) [here](simulating_attacker_authentication_events_using_linux.md).

---

## Investigation Process

The investigation included:

- Verifying that `systemd-journald` was running
- Searching authentication events
- Identifying failed logins
- Identifying successful logins
- Extracting usernames
- Reviewing source IP addresses
- Counting repeated authentication attempts
- Assessing whether activity appeared suspicious

---
## Key Findings

- Multiple failed authentication attempts
- Successful SSH logins after failed attempts
- Authentication events from localhost (`127.0.0.1`)
- Activity resembled a password guessing attack
- Determined to be a controlled lab exercise

---
## Sample Screenshots

### Verifying the Logging Service
<img width="868" height="165" alt="image" src="https://github.com/user-attachments/assets/251ef6a8-4953-4f08-bd30-9839ac19271a" />

---

### Failed SSH Login

<img width="943" height="248" alt="image" src="https://github.com/user-attachments/assets/3c678d13-f076-4e29-861c-0b936742b79e" />

---

### Successful SSH Login

<img width="916" height="139" alt="image" src="https://github.com/user-attachments/assets/f478fac2-04d4-48cb-ae7a-2b0c41995f96" />

---

### Authentication Log Investigation

<img width="934" height="211" alt="image" src="https://github.com/user-attachments/assets/65d86411-57c1-4352-8635-7152025ab6c3" />

---

## Skills Demonstrated

- Linux Administration
- Authentication Log Analysis
- SSH Investigation
- sudo Investigation
- journalctl
- grep
- Log Filtering
- Security Event Analysis
- Incident Documentation

---

## Conclusion
Although all authentication events were intentionally generated as part of this controlled laboratory exercise, the observed pattern closely resembles a brute-force or password guessing attack. In a production environment, this activity would warrant further investigation, including validating successful logins, reviewing affected accounts, and determining whether containment actions are required.

---

## Full Documentation

📄 **Complete investigation report (pdf):**  
[SOC Lab 1: Investigating Linux Authentication Logs](SOC%20Lab%201%20%E2%80%93%20Investigating%20Linux%20Authentication%20Logs.md)

