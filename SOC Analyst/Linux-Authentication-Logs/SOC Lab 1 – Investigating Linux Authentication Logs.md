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

x
