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

_Answer: poisonivy-is-coming-for-you-batman.jpeg_

##### Attach Chain Analysis:

1. Attacker used web vulnerability scanner (Acunetix) and found vulnerable in Joomla component flaw which later used  the vulnerability to exploits that let them get remote code execution or a remote file inclusion (RFI) on the server.  The victim server acts as the "puller," not the attacker as the "pusher."
2. Instead of directly uploading the file via a form, they made the compromised server itself fetch the malicious image from their own external server
3. The website then served/displayed that fetched image, defacing the site.

---

**Question 5: This attack used dynamic DNS to resolve to the malicious IP. What fully qualified domain name (FQDN) is associated with this attack?**

I tried to use the source type specifically the `stream:dns` but I have a difficult time to find the domain name. Instead, I still used the HTTP logs from source type `stream:http`. But we already found the domain name from the question 4. Anyways, let confirm using this spl commands:

```
index=botsv1 sourcetype=stream:http src_ip=192.168.250.70 dest_ip=23.22.63.114
| rename site AS domain_name
| table _time, domain_name, uri_path
| sort _time
```

This query searches all indexes for HTTP traffic from the website IP `192.168.250.70` to malicious external IP `23.22.63.114` used by the attacker, rename the site as domain_name for easy identify the domain name, display it in a table, and sort by time.

<img width="1807" height="573" alt="image" src="https://github.com/user-attachments/assets/96953ac9-abe0-4ff8-9960-0da10266fe5c" />

- From the search result,  the domain name of the malicious IP `23.22.63.114` is the `prankglassinebracket.jumpingcrab.com:1337`. I can confirmed this is the right answer because under the uri_path the `poisonivy-is-coming-for-you-batman.jpeg` is the defacement image from the attacker's external hosting site.

_Answer: prankglassinebracket.jumpingcrab.com:1337_

---

**Question 6: What IPv4 address has Po1s0n1vy tied to domains that are pre-staged to attack Wayne Enterprises?**

We already found the IPv4 address where Po1s0n1vy tied to domains.

_Answer: 23.22.63.114_

---

**Question 7: What IPv4 address is likely attempting a brute force password attack against imreallynotbatman.com?**

Brute force attempts show up as repeated POST requests to the Joomla admin login endpoint from the same source, usually in rapid succession with varying credentials. I use this spl commands:

```
index=* sourcetype=stream:http dest_ip=192.168.250.70 uri_path="*administrator*" http_method=POST
| stats count by src_ip
| sort - count
```
This query searches all indexes for HTTP POST requests to the Joomla administrator login page on destination IP 192.168.250.70, counts how many requests came from each source IP, and sorts the results to highlight the most active attackers

<img width="1913" height="505" alt="image" src="https://github.com/user-attachments/assets/2dcafeb4-cbef-4bd7-ad97-1893c0900176" />

We can see `23.22.63.114` with a very high count of  requests to the admin login page. That volume of repeated login attempts in a short window is the signature of a brute force attack. To confirm the brute force attacks, lets pivot to `POST` requests by using the fields `byte`. Run in this next:

```
index=* sourcetype=stream:http src_ip=23.22.63.114 dest_ip=192.168.250.70 http_method=POST
| stats count by status, bytes
| sort - count
```

We can see the actual brute force attempts. Every row is `status=303`. For example, Joomla redirects after processing a login POST, whether it succeeds or fails, and the `bytes` values are all clustered tightly in the **852–856** range. That tight clustering is exactly what a failed login attempt looks like where Joomla redirects you back to the login form with an error each time.

<img width="1911" height="698" alt="image" src="https://github.com/user-attachments/assets/35f7f7c2-6de0-4b70-a579-d47ab1a4b7ea" />

- From the search result, every other byte-size value (852–856) has dozens or hundreds of occurrences and the a normal repeated "failed login" response. But `857` appears **exactly once**, breaking the pattern entirely. That's almost certainly your successful login response. Lets confirm again using these spl commands:

```
index=* sourcetype=stream:http src_ip=23.22.63.114 dest_ip=192.168.250.70 http_method=POST bytes=857
| table _time _time, uri_path, status, bytes, form_data
```

<img width="1920" height="512" alt="image" src="https://github.com/user-attachments/assets/ff80b6a8-0f1e-459f-868f-3606a765832d" />

- The output shows full confirmation that it is a a brute force attacks. 

##### Successful brute force credentials
- Username:** `admin`
- Password:** `123456789`
- Timestamp:** `2016-08-10 21:45:25.299`

##### Why this is the confirmed successful attempt
- It's the **only** POST response with `bytes=857` while every other attempt (852–856 bytes) was a failed-login redirect back to the same login form.
- The distinct byte count means Joomla returned a different response this time — consistent with a successful auth redirecting to the admin dashboard instead of back to the login page
- `passwd=123456789` fits the same "common weak password" wordlist pattern that easily to brute force.

The same IP (`23.22.63.114`) tying together the scanning infrastructure, the malicious file-hosting domain, and now the brute force attempts strongly indicates this is Po1s0n1vy's primary attack IP throughout the whole campaign.

_Answer: 23.22.63.114._

----

**Question 8: What is the name of the executable uploaded by Po1s0n1vy?**

In this part, I check every values in each fields to see if there is any executable file payloads ending with `.exe`.

<img width="1247" height="801" alt="image" src="https://github.com/user-attachments/assets/3efe0a64-4293-400b-90d3-44055358c6be" />

I found `3791.exe` from the part_filename{} fields. To confirm this is the executable uploaded by Po1s0n1vy, I use this spl commands:

```
index=* sourcetype=stream:http dest_ip=192.168.250.70 http_method=POST part_filename{}="3791.exe"
| table _time, c_ip, dest_ip, http_comment, http_method, part_filename{}, http_content_type
| sort _time
```

This query searches all indexes for HTTP POST requests to destination IP 192.168.250.70 where the uploaded file is 3791.exe, then displays detailed fields in a table and sorts them chronologically by time.

<img width="1906" height="463" alt="image" src="https://github.com/user-attachments/assets/5467a513-7f85-4278-a1b9-b6490cdafe85" />

- From the result, `part_filename{}` field has a both `3791.exe` and `agent.php` that show up in a signgle event. It tells attacker uploaded a simultaneously in one multipart form POST likely through Joomla media manager or template editor, where an attacker can bundle multiple files into a single upload request.

_Answer: 3791.exe_

---
**Question 9: What is the MD5 hash of the executable uploaded?**

MD5 is a cryptographic hash and cannot be found in the HTTP traffic (`stream:http`). To get the hash, Windows server is the needed source type,  since Sysmon records the MD5 of any executable it sees run.

<img width="731" height="737" alt="image" src="https://github.com/user-attachments/assets/a64fdd80-4d00-4921-a66d-b42a6ba1e8d7" />
let's try this source type `XmlWinEventLog:Microsoft-Windows-Sysmon/Operational`

```
index=* sourcetype=XmlWinEventLog:Microsoft-Windows-Sysmon/Operational EventCode=1 "3791.exe"
| table _time, host, Image, CommandLine, Hashes
```
This query searches all indexes for Sysmon EventCode 1 (process creation) events where the executable 3791.exe was run, then displays details such as time, host, image path, command line, and file hashes.

<img width="1873" height="647" alt="image" src="https://github.com/user-attachments/assets/ebaa2ee0-6166-48d2-a4ef-8b0a2049d441" />

From the search result, we can see the `3791.exe` use as the executable payloads and the md5 cryptographic hash on the hashes fields. That execution confirmation is critical: it shows the attack succeeded beyond just placing the file — Po1s0n1vy achieved actual code execution, not just an upload.

_Answer: AAE3F5A29935E6ABCC2C2754D12A9AF0_

