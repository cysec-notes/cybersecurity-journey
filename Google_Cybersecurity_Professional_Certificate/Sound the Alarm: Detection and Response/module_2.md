# Module 2: Network Monitoring and Analysis
## Overview

## Learning Objectives
-  Network traffic flows
-  packet sniffers
-  packet analysis

## Key Concepts I Learned
1. Network traffic is the amount of data that moves across a network.
2. Network data is the data that's transmitted between devices on a network.

**Indicators of compromise**, also known as IoC, which are observable evidence that suggests signs of a potential security incident.
**data exfiltration**, which is the unauthorized transmission of data from a system.


[Learn about wireshark](https://www.wireshark.org/docs/wsug_html/)

#### Defensive measures
1. prevent attacker access
2. monitor network activity
3. protect assets
4. detect and stop the exfiltration

A packet capture, or P-cap, is a file containing data packets intercepted from an interface or network.

#### Packets contain three components: the header, the payload, and the footer. 
1. Header
2. Payload
3. Footer


A **network protocol analyzer (packet sniffer)** is a tool designed to capture and analyze data traffic within a network.

**Packet sniffing** is the practice of capturing and inspecting data packets across a network. 

#### Activity: Analyze your first packet
In this lab activity, I learned capture and analyze live network traffic using tcpdump.

- Identify available network interfaces
- Use tcpdump to capture live network traffic
- Save network traffic to a packet capture file
- Filter the packet capture data

#### Incident response tools
- detection and management tools
- documentation tools to collect and compile evidence.
- investigative tools for analyzing these events, like packet sniffers.
- 
## Personal Reflection
<img width="708" height="661" alt="image" src="https://github.com/user-attachments/assets/b452210c-1713-470a-81c7-1899a7d641b8" />

**Some of my key takeaways:**
Tcpdump is also like Linux sort of.  I learned how to identify network interfaces, use the tcpdump command to capture network data for inspection,
interpret the information that tcpdump outputs regarding a packet, and save and load packet data for later analysis. Tcpdump is used data in a packet capture (p-cap) file. https://www.skills.google/focuses/50128118?parent=lti_session

**-w, -r, -v, -c**: I learned this three command used in tcpdump. "w" to write or safe in file. "r" to read the file. "v" to see detailed. "c" to count packets.

  
## Next Steps
[Continue Course 5 Module 2](module_2.md)






