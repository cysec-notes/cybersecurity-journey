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

- The searched returned all sourced IP address found in the website. `40.80.148.42` has an overwhelming majority of the events (20,932 hits). That volume pattern is more likely the IPv4 address of someone from the Po1s0n1vy group. We have a second ip found `23.22.63.114` that we will investigate later.


_Answer: 40.80.148.42_

---

**Question 2: What company created the web vulnerability scanner used by Po1s0n1vy? Type the company name.**

We already find the attacker's IP address `40.80.148.42`. In this part, an attacker used a web scanner to find any vulnerabilities in the website likely to be exploit. To identify the company vulnerability scanner, we need to look at the HTTP request coming from that IP and find the User-Agent used by the scanner. I use these SPL commands:

```
index=botsv1 sourcetype=stream:http src_ip=40.80.148.42
| dedup http_user_agent
| table http_user_agent
| stats count by http_user_agent
```
This query searches the botsv1 index for HTTP traffic `sourcetype=stream:http` from the source IP `40.80.148.42`. In addition, we use the `dedup` commands to remove any duplication from the specific field `http_user_agent`, make a table to that field, and counts the number of events to show what web vulnerability scanner used. 

<img width="1023" height="805" alt="image" src="https://github.com/user-attachments/assets/eb044247-8c3f-4da1-99b1-94a9ec4701ad" />

- From the search result, looking at the `http_user_agent` values, some entry stands out; '${@print(md5(acunetix_wvs_security_test))}'. This is a PHP code injection test payload. Notice it literally contains the string `acunetix_wvs` — this isn't coincidental. It's a known signature payload that the Acunetix Web Vulnerability Scanner (WVS) injects during its automated scanning to test for PHP code execution vulnerabilities (if the target is vulnerable, the app would execute `md5()` on the string and reflect a hash back, confirming code injection). Let's investigate this later.

_Answer: Acunetix_

---

**Question 3: What content management system is imreallynotbatman.com likely using?**

I determined the cms using the fields `uri_path` that identifies a target resource or page on a server. This spl commands I used:

```
index=botsv1 sourcetype=stream:http src_ip=40.80.148.42
| stats count by uri_path
| sort - count
```

This query searches the botsv1 index for HTTP traffic from source IP 40.80.148.42, counts how many times each URI path was accessed, and then sorts the results to show the most frequently requested paths first."

<img width="824" height="711" alt="image" src="https://github.com/user-attachments/assets/3a86c84e-b80f-4330-97a0-979b4e11ec31" />

- Based on this output, it's confirmed: imreallynotbatman.com is running Joomla. `/joomla/index.php/component/search/` hits 16,667 hits and `/joomla/administrator/index.php` hits 33 hits. That massive count is very likely Acunetix fuzzing the Joomla search component for injection points. Search forms are a classic target since user input gets passed into a query, making them prime candidates for SQLi/XSS testing.

In this search I found suspicious uri_path commonly known as traversal attack.

<img width="1458" height="77" alt="image" src="https://github.com/user-attachments/assets/a9be6226-97ad-453b-956a-30dac2a1a7b4" />

I also notice the scanner tried:

- `/windows/win.ini`
- `/boot.ini`
- `/windows/win.ini%00.jpg` (null-byte injection attempt)
- A massive directory-traversal string (`.\.\.\.\.\.\.` repeated) trying to walk up to `win.ini`

This traffic pattern is strong supporting evidence that the CMS is **Joomla**. You can see exploitation attempts against Joomla specifically (the `/joomla/administrator/index.php` path nearby is the Joomla admin login)

_Answer: Joomla_

---

Question 4: What is the name of the file that defaced the imreallynotbatman.com website? 

This ties directly into the earlier steps of the investigation after Po1s0n1vy's Acunetix scan identified the Joomla CMS and its vulnerabilities, they exploited a Joomla component vulnerability. 

Let us find first host IP or the website IP address using these spl commands:

```
index=* sourcetype=stream:http imreallynotbatman.com
| stats count by dest_ip
```
<img width="1904" height="426" alt="image" src="https://github.com/user-attachments/assets/f8fb3879-e307-444f-ae76-2c004388973c" />

- The search returned that host ip address `192.168.250.70`. Website defacements typically involve an attacker uploading a new file that replaces or sits alongside the normal site content. Let use these spl commands to see what file does Po1s0n1vy upload in the website.

```
index=* sourcetype=stream:http src_ip=192.168.250.70
| table _time, dest_ip, dest_port, site, uri_path
| sort _time
```
This query searches all indexes for HTTP traffic from source IP 192.168.250.70, displays key connection details in a table, and sorts the results chronologically by time.

<img width="1856" height="764" alt="image" src="https://github.com/user-attachments/assets/6ebe299c-4723-49a0-a798-554ec526268f" />

- From the search result, the web server itself `192.168.250.70` (imreallynotbatman.com's own server) reached out to fetch this file  sent a `GET` request to  an external host `23.22.63.114` on port `1337`, pulling the defacement image down from the attacker's external hosting site `prankglassinebracket.jumpingcrab.com`. These second IP address `23.22.63.114` from question 1, where I found a suspicious one are confirmed really malicious.

##### Attach Chain Analysis:

1. Attacker used web vulnerability scanner and found vulnerable in Joomla component flaw which later used  the vulnerability to exploits that let them get remote code execution or a remote file inclusion (RFI) on the server.  The victim server acts as the "puller," not the attacker as the "pusher."
2. Instead of directly uploading the file via a form, they made the compromised server itself fetch the malicious image from their own external server
3. The website then served/displayed that fetched image, defacing the site.
