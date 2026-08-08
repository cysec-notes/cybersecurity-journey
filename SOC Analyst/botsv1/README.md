# Boss of the SOC v1 Investigation Version 1 (2015) 
Welcome! this repository contains my complete walkthrough of BOSS of the SOC (BOTS) Version 1 – Scenario 1: **Web Defacement** &  Scenario 2: **Ransomware** (https://bots.splunk.com/).

This project serves as both a walkthrough and a personal home lab where I practice using Splunk Enterprise, improve my SPL (Search Processing Language) skills, and gain hands-on experience with the incident response process. **My goal is not only to solve the challenge but also to think and investigate like a SOC Analyst.**

While working through this scenario, I found many walkthroughs online that simply provided the answers or screenshots with brief explanations. However, I wanted to understand how those answers were actually discovered. Not just what the answers were, but also the thought process, SPL queries, evidence, and conclusions that led to each finding.

Aside this walkthrough, I also created an [Incident Report for Web Defacement](Incident%20Report%20—%20BOTS%20v1%20Web%20Defacement.pdf) to demonstrate my ability to document security incidents and communicate investigation findings in a structured report.

### Scenario 1: Web Site Defacement
Today is Alice's first day at the Wayne Enterprises' Security Operations Center. Lucius sits Alice down and gives her first assignment: A memo from Gotham City Police Department (GCPD). Apparently GCPD has found evidence online (http://pastebin.com/Gw6dWjS9) that the website www.imreallynotbatman.com hosted on Wayne Enterprises' IP address space has been compromised. The group has multiple objectives... but a key aspect of their modus operandi is to deface websites in order to embarrass their victim. Lucius has asked Alice to determine if www.imreallynotbatman.com. (the personal blog of Wayne Corporations CEO) was really compromised.

### Scenario 2: Ransomware
After the excitement of yesterday, Alice has started to settle into her new job. Sadly, she realizes her new colleagues may not be the crack cybersecurity team that she was led to believe before she joined. Looking through her incident ticketing queue she notices a “critical” ticket that was never addressed. Shaking her head, she begins to investigate. Apparently on August 24th Bob Smith (using a Windows 10 workstation named we8105desk) came back to his desk after working-out and found his speakers blaring (click below to listen), his desktop image changed (see below) and his files inaccessible. Alice has seen this before... ransomware. After a quick conversation with Bob, Alice determines that Bob found a USB drive in the parking lot earlier in the day, plugged it into his desktop, and opened up a word document on the USB drive called "Miranda_Tate_unveiled.dotm". With a resigned sigh she begins to dig into the problem...


### Lab Objective: 
- Find any current anomalies in the network and see if Wayne Enterprises has been previously compromised.
- Identify any critical assets that have sensitive data
- Find any unauthorized access
- Identify Indicator of Compromise (IoC)

## Skills develop
- SPL & Splunk searching
- Threat Hunting
- IOC Analysis
- Log Analysis
- Web attack analysis
- Windows log analysis
- Digital evidence collection
- Incident Reporting
- 

## Tools used:
- Splunk Enterprise
- BOTS v1 Dataset
- VirusTotal
- CyberChef

## Investigation Process
1. Identified attacker IP
2. Investigated web attacks
3. Found brute-force activity
4. Identified malware download
5. Correlated Windows events
6. Built attack timeline
7. Documented indicators


