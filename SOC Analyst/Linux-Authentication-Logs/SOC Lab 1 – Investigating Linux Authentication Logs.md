# Investigation Report — Linux Auth Log Review
Date: July 03, 2026 | Analyst: Cyrish Lerio

### Summary
In this hands-on controlled lab, I intentionally generated authentication events to produce logs for analysis using Linux commands to investigate like a SOC Analyst in a pretend real-life situations. To determine whether these authentication events are normal user activity or something suspicious.

### Timeline
Example:

| Timestamp                  | Event                       | Username |
| -------------------------- | --------------------------- | -------- |
| Jul 03 11:47:41 - 11:47:58 | sudo authentication failure | -        |
| Jul 03 11:47:59 - 11:48:11 | Failed login (invalid user) | baduser  |
| Jul 03 11:48:11 - 11:48:47 | sudo authentication failure |          |
| Jul 03 11:48:48 - 11:48:59 | Failed login                | cy       |
| Jul 03 11:56:44 - 11:56:47 | Successful SSH login        | cy       |
<img width="900" height="235" alt="image" src="https://github.com/user-attachments/assets/c4473317-06a6-4940-ad23-69454b97208f" />

### Findings
Total failed attempts:

<img width="358" height="120" alt="image" src="https://github.com/user-attachments/assets/ab18a443-e05a-41c7-b324-eebb680d9766" />

Usernames targeted: 

<img width="763" height="214" alt="image" src="https://github.com/user-attachments/assets/5fc58c29-7f2c-445e-ab22-4156a13fb0fe" />

Successful logins: 

<img width="810" height="190" alt="image" src="https://github.com/user-attachments/assets/3eb4fcc2-2897-4ec5-8ec0-e2f3ef7978ec" />
- All source IP(s): 127.0.0.1 (this is only a test)

 ### Assessment
Since, I generated different login attempt, the logs results show rapid authentication login attempts within a short period. These include multiple failed or success login attempts where both valid and non-existent usernames is from a single IP address (127.0.0.1) that targeting accounts. This pattern resembles a password guessing or brute-force attack. Even though the activity is from localhost as part of a controlled lab, the severity is medium because this can be a similar behavior of malicious activity. Therefore, to determine whether the successful logins were authorized or not, this log analysis should be flagged as suspicious and needs further investigation.

### Evidence
Let's check in the journalctl if logs was generate to verify that the events were successfully recorded.

<img width="945" height="211" alt="image" src="https://github.com/user-attachments/assets/d2630629-bc67-434f-9680-a1dadd197938" />

- _Confirmed it collects and records the event and shows authentication event_

Success:

<img width="765" height="162" alt="image" src="https://github.com/user-attachments/assets/e03673da-ca60-4447-b7a0-29646962d88a" />

Failures (failed password/incorrect password):

<img width="953" height="268" alt="image" src="https://github.com/user-attachments/assets/6162ccf8-598b-48e1-9c49-3c51a0997580" />

Su/sudo outcomes if authentication failure or session opened

<img width="946" height="171" alt="image" src="https://github.com/user-attachments/assets/01805869-63e3-4088-9df0-eb7e11fce22a" />

Failed login attempts by username in ssh

<img width="246" height="134" alt="image" src="https://github.com/user-attachments/assets/6ac32fab-daae-49dc-93d2-8801bf33af4d" />

Failed login attempts by source IP

<img width="470" height="127" alt="image" src="https://github.com/user-attachments/assets/ea4447cb-4995-4d0b-a260-2c4cb64d1739" />

Successful logins by username

<img width="470" height="141" alt="image" src="https://github.com/user-attachments/assets/83aace38-2533-49e6-b208-62c470cf9fa7" />

### Recommendation
No action needed, this only a self-testing. However in a real-life scenario, cybersecurity team should use a firewall or IDS/IPS to block repeated failed login attempts from suspicious sources. Enforcing password policy such as making a stronger password, add multi-factor authentication for another verification, and limit logging attempts by locking accounts after after a set number of failed. Set up SIEM rules for monitoring and alerts security analyst. Lastly, conduct regular log audits to review, identify trends or anomalies, and potential insider threats.
