# Botsv1 Web Defacement: Complete Investigation Walkthrough
 This is where analysts investigate a simulated cyberattack where an unauthorized user changes a company website's visual appearance and how I found the answers. 

#### Understand the Incident
Reports indicate that the website www.imreallynotbatman.com has been compromised specifically through web defacement. 
My first objective is to determine if the website was really compromised. If confirmed, I will determine when the attack occurred and identify the affected web server.

Since this is a web defacement, the attacker most likely interacted with the web server using HTTP. I decided to begin by examining HTTP logs. However, I don't know what source type it is in our Splunk. Splunk used to investigate and solve simulated real-world cyberattacks where it collects, indexes, and analyzes massive volumes of machine-generated data. let us confirm first by this spl query:

```
index=botsv1 imreallynotbatman.com
| stats count by sourcetype
| sort - count
```
This query searches across all indexes of 'botsv1' but filters the results to find all sourcetype.

<img width="1907" height="595" alt="image" src="https://github.com/user-attachments/assets/c7cc8e21-1506-4c56-b5ba-070680cc032c" />
- Most likely the sourcetype I need is the 'sourcetype=stream:http' where all HTTP logs are records.
