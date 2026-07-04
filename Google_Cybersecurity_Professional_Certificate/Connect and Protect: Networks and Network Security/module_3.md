# Module 3: Secure against network intrusions
## Overview
You will understand types of network attacks and techniques used to secure compromised network systems and devices. You'll explore the many ways that malicious actors exploit vulnerabilities in network infrastructure and how cybersecurity professionals identify and close potential loopholes.

## Learning Objectives
After completing this module, I can:
- Network Security
- Network intrusion tactics
- Network attack protection

## Key Concepts Learned
**Botnet**: A collection of computers infected by malware that are under the control of a single threat actor, known as the “bot-herder"

**Denial of service (DoS) attack**: An attack that targets a network or server and floods it with network traffic While the **Distributed denial of service (DDoS)** attack: A type of denial of service attack that uses multiple devices or servers located in different locations to flood the target network with unwanted traffic

Types of DoS attack:
1. **Synchronize (SYN) flood attack**: A type of DoS attack that simulates a TCP/IP connection and floods a server with SYN packets
2. **Internet Control Message Protocol (ICMP) flood**: A type of DoS attack performed by an attacker repeatedly sending ICMP request packets to a network server
3. **Ping of death**: A type of DoS attack caused when a hacker pings a system by sending it an oversized ICMP packet that is bigger than 64KB

**Internet Control Message Protocol (ICMP)**: An internet protocol used by devices to tell each other about data transmission errors across the network

**Packet sniffing:** The practice of capturing and inspecting data packets across a network 
1. Passive packet sniffing: A type of attack where a malicious actor connects to a network hub and looks at all traffic on the network
2. Active packet sniffing: A type of attack where data packets are manipulated in transit

**IP spoofing:** A network attack performed when an attacker changes the source IP of a data packet to impersonate an authorized system and gain access to a network
1. On-path attack: An attack where a malicious actor places themselves in the middle of an authorized connection and intercepts or alters the data in transit
2. Replay attack: A network attack performed when a malicious actor intercepts a data packet in transit and delays it or repeats it at another time
3. Smurf attack: A network attack performed when an attacker sniffs an authorized user’s IP address and floods it with ICMP packets

## Personal Reflection
In this module I discovered some network attacks, its negative impact, and how to prevent those attacks. One of the negative impact of network attaks are; financial loss, reputation damage to the organization, and public safety  (attack → disruption → loss of trust → migration to competitors → long-term damage to the original organization). I learned how VPN was important to secure our data packets across networks so that if some malicious actors capture our packet, the sensitive information will not disclosed because of enncryption. Preventing a DoS or DDoS attack can also be avoide through firewall configuration, to blocked suspicious activity (source IP add). I learn to read events in a logs from tcpdump and wireshark. This module also provide a comprehensive practice about network analysis and incident report using tools for capturing data packets (tcpdumps & wiresharks). Lastly, I learn how to analyze and response to a cyber attack incidents. 
## Next Steps
Continue Course 1 Module 2


