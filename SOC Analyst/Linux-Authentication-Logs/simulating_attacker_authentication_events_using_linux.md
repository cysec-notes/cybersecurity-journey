# SOC Lab 1 – Simulating Attacker Authentication Events: Investigating Linux Authentication Logs

## Authentication Events Generated

To simulate realistic attacker activity, I deliberately triggered a variety of authentication events on the Linux system. These included failed and successful login attempts through both local and remote (SSH) access, as well as privilege escalation attempts using `sudo`. By mixing successful and failed authentications, the dataset reflects common attack patterns such as brute-force attempts, unauthorized access, and privilege misuse.  

These events were later examined through Linux log analysis, providing clear visibility into how malicious behavior is recorded and how a SOC analyst can trace suspicious activity back to its source.
