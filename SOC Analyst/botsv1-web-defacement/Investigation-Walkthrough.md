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

- The searched returned all the source type from different source. Most likely the source type I need is the `sourcetype=stream:http` where all HTTP logs are records.

**Question 1**: What is the likely IPv4 address of someone from the Po1s0n1vy group scanning imreallynotbatman.com for web application vulnerabilities?

Using the `sourcetype=stream:http` and website `imreallynotbatma`, we can determine what IP address from the attacker group. I use this spl query to find the source IP:

```
index=botsv1 sourcetype=stream:http imreallynotbatman
| stats count by src_ip
| sort - count
```

This query searches the botsv1 index for HTTP traffic `sourcetype=stream:http` related to the website imreallynotbatman, counts the number of events grouped by source IP `src_ip`, and then `sorts` the results to show the IPs with the highest activity first.

<img width="1907" height="557" alt="image" src="https://github.com/user-attachments/assets/1c9a8570-04d8-4b13-80ac-e3534c4e5a0c" />

- The searched returned all sourced IP address found in the website. `40.80.148.42` has an overwhelming majority of the events (20,932 hits). That volume pattern is more likely the IPv4 address of someone from the Po1s0n1vy group.

_Answer: 40.80.148.42_

---

**Question 2: What company created the web vulnerability scanner used by Po1s0n1vy? Type the company name.**

We already find the attacker's IP address `40.80.148.42`. In this part, an attacker used a web scanner to find any vulnerabilities in the website likely to be exploit.

- **Look at the HTTP requests coming from that IP.**  **Find the User-Agent** used by the scanner. **Identify the vulnerability scanner.** **Determine the company that created that scanner.**
