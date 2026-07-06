
---
# SOC Lab 1 – Investigating Linux Authentication Logs
From the TryHackMe platform and its available walkthrough rooms, I familiarized myself first with some concepts and fundamentals of log management, types, format, collection, storage, etc. to prepare for this lab. Before delving into actual SIEM tools used by SOC analysts such as Splunk, I understand first what is logs, how it works, where it stores, and how to analyze using Linux commands. 

As a beginner, I created this hands-on lab to gain knowledge, familiarize myself, learn through experience like in a real world scenario and  discover commands using the Linux system.

---
### <span style="color:rgb(255, 192, 0)">Objectives:</span>
By the end of this lab, I should be able to:
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

You are a Tier 1 SOC Analyst at a company. 

At 11:00 AM, the Security Operations Center receives this alert: 

<span style="color:rgb(255, 0, 0)">"Multiple authentication events were detected on the Linux server overnight."</span>


Your team lead asks:

<span style="color:rgb(0, 176, 240)">"Determine whether these authentication events are normal user activity or something suspicious."</span>

You have access only to the Linux server. Your job is to investigate using system logs.

---


### <span style="color:rgb(255, 192, 0)">Understand Concept</span>
**What is logs:**
Logs is a record of events (like a reciept).

**What does authentication mean?** 
It means to verify a user's identity before letting them access.

**What kinds of authentication events can happen?** 
Success logins, failed login, sudo, ssh login, su

**Where does Linux keep authentication events?** 
I am using **Kali Linux with `systemd-journald` (no `rsyslog`)**, authentication logs are stored in the **systemd journal**, not in `/var/log/auth.log`

### <span style="color:rgb(255, 192, 0)">Checking if the system-journald is running:</span>
![[Pasted image 20260702175846.png]]
*system is active and running and ready to be collect.*

### <span style="color:rgb(255, 192, 0)">Generate authentication events ( as attacker)</span>
I open the two terminals in my linux. One to generate events, one is to investigate.

*Failed local login attempts*
![[Pasted image 20260702183510.png]]

![[Pasted image 20260703114255.png]]

To test SSH, I first enabled it on my localhost and then verified that the service was running.
![[Pasted image 20260702202752.png]]

*Failed SSH attempts*
![[Pasted image 20260702202858.png]]

*Successful  SSH login attempts*
![[Pasted image 20260702202929.png]]


*Sudo events (successful and failed)*
![[Pasted image 20260702185542.png]]
![[Pasted image 20260702185723.png]]

I repeated these login attempts , both successful and failed, to generate logs that we can investigate later. In this way we can identify different logs and investigate the events if it is a normal activity or suspicious.

----

# Investigation Report — Linux Auth Log Review
Date: July 03, 2026
Analyst: Cyrish Lerio

## Summary
In this hands-on controlled lab, I intentionally generated authentication events to produce logs for analysis using Linux commands to investigate like a SOC Analyst in a pretend real-life situations. To determine whether these authentication events are normal user activity or something suspicious.

## Timeline
Example:

| Timestamp                  | Event                       | Username |
| -------------------------- | --------------------------- | -------- |
| Jul 03 11:47:41 - 11:47:58 | sudo authentication failure | -        |
| Jul 03 11:47:59 - 11:48:11 | Failed login (invalid user) | baduser  |
| Jul 03 11:48:11 - 11:48:47 | sudo authentication failure |          |
| Jul 03 11:48:48 - 11:48:59 | Failed login                | cy       |
| Jul 03 11:56:44 - 11:56:47 | Successful SSH login        | cy       |


![[Pasted image 20260703170054.png]]
## Findings
Total failed attempts:
![[Pasted image 20260703163611.png]]

Usernames targeted: ![[Pasted image 20260703152849.png]]

Successful logins: 
![[Pasted image 20260703164101.png]]

 All source IP(s): 127.0.0.1 (this is only a test)

## Assessment
Since I generated different login attempt, the logs results show rapid authentication login attempts within a short period. These include multiple failed or success login attempts where both valid and non-existent usernames is from a single IP address (127.0.0.1) that targeting accounts. This pattern resembles a password guessing or brute-force attack. Even though the activity is from localhost as part of a controlled lab, the severity is medium because this can be a similar behavior of malicious activity. Therefore, to determine whether the successful logins were authorized or not, this log analysis should be flagged as suspicious and needs further investigation.

## Evidence

Let's check in the journalctl if logs was generate to verify that the events were successfully recorded.
![[Pasted image 20260703133422.png]]
Confirmed it collects and records the event and shows authentication event

Success:
![[Pasted image 20260703133706.png]]

Failures (failed password/incorrect password):
![[Pasted image 20260703133957.png]]

Su/sudo outcomes if authentication failure or session opened
![[Pasted image 20260703134115.png]]

Failed login attempts by username in ssh
![[Pasted image 20260703140335.png]]

Failed login attempts by source IP
![[Pasted image 20260703140603.png]]

Successful logins by username
![[Pasted image 20260703140701.png]]


## Recommendation
No action needed, this only a self-testing. However, in a real-life scenario I recommend to block source IP (suspicious one) and forcing password reset for targeted accounts.
