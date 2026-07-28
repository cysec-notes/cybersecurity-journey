# Simulating Attacker Authentication Events

To simulate realistic attacker activity, I deliberately triggered a variety of authentication events on the Linux system. These included failed and successful login attempts through both local and remote (SSH) access, as well as privilege escalation attempts using `sudo`. By mixing successful and failed authentications, the dataset reflects common attack patterns such as brute-force attempts, unauthorized access, and privilege misuse.  

These events were later examined through Linux log analysis, providing clear visibility into how malicious behavior is recorded and how a SOC analyst can trace suspicious activity back to its source.


### Understanding Concept
**What is logs:**
- Logs is a record of events (like a reciept).

**What does authentication mean?** 
- It means to verify a user's identity before letting them access.

**What kinds of authentication events can happen?** 
- Success logins, failed login, sudo, ssh login, su

**Where does Linux keep authentication events?** 
- I am using **Kali Linux with `systemd-journald` (no `rsyslog`)**, authentication logs are stored in the **systemd journal**, not in `/var/log/auth.log`

### Checking if the system-journald is running:
<img width="653" height="122" alt="image" src="https://github.com/user-attachments/assets/a17993a3-c75e-408d-8243-a45e7679ef07" />

- _system is active and running and ready to be collect._

### Generate authentication events ( as attacker)
  I open the two terminals in my linux. One to generate events, one is to investigate.

*Failed local login attempts*

<img width="844" height="70" alt="image" src="https://github.com/user-attachments/assets/9b050011-fd5f-45e6-a2a1-4e8f6be191bd" />

<img width="312" height="137" alt="image" src="https://github.com/user-attachments/assets/ba20b6dd-dd0d-4edf-9979-1a310b10e42a" />

To test SSH, first, I enabled it on my localhost and then verified that the service was running.

<img width="707" height="171" alt="image" src="https://github.com/user-attachments/assets/3a7ad0c8-0462-4ecf-8ea9-84a2ef77dcac" />

*Failed SSH attempts*

<img width="497" height="146" alt="image" src="https://github.com/user-attachments/assets/43f7d3b2-0062-4593-8cee-d9a9bbcfa966" />

*Successful  SSH login attempts*

<img width="792" height="347" alt="image" src="https://github.com/user-attachments/assets/f1a05a2c-5499-4e2c-928c-6504548c7029" />

*Sudo events (successful and failed)*

<img width="218" height="181" alt="image" src="https://github.com/user-attachments/assets/3dd89a61-e414-47cc-8a92-741cf5f9ed25" />
<img width="312" height="151" alt="image" src="https://github.com/user-attachments/assets/6e7bc0ae-3f9f-43ed-b7ab-b7e7e3331480" />

I repeated these login attempts , both successful and failed, to generate logs that we can investigate later. In this way we can identify different logs and investigate the events if it is a normal activity or suspicious.

You can check my complete report [here](SOC%20Lab%201%20%E2%80%93%20Investigating%20Linux%20Authentication%20Logs.md) 

