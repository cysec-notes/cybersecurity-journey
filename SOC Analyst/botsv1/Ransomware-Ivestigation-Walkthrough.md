# Botsv1 Ransomware: Complete Investigation Walkthrough

This repository documents my complete investigation of the Boss of the SOC (BOTS) v1 Ransomware scenario. Rather than presenting only the challenge answers, I document my investigative methodology, the SPL queries I used, my reasoning at each step, and the evidence that led to each conclusion.

#### Understand the Incident
On August 24th, an employer of Wayne Enterprise, Bob Smith, report that his workstation had been compromised. His speakers were playing a ransomware message stating that his documents, photos, databases, and other important files had been encrypted. His desktop background had also been changed, and he was unable to access his files.

According to Bob, the incident began after he found a USB drive in the parking lot. He connected the USB device to his workstation and opened a Microsoft Word document named Miranda_Tate_unveiled.dotm.

The use of a suspicious USB device followed by the execution of a macro-enabled Word document is a significant indicator of potential malware execution and ransomware incident requiring urgent investigation

An additional concern was also identified in the incident ticketing queue: a critical security ticket had been created but had not been addressed. This may indicate that an earlier warning or security alert was missed, potentially allowing the attacker to continue their activity.

---

**Question 1: What was the most likely IPv4 address of we8105desk on 24AUG2016?**

During the interview, Bob Smith state he was using a Windows 10 workstation named `we8105desk`. 

To identify the IPv4 address on 24 August 2016, I used the host name `we8105desk`. The following is my spl query.

```
index=botsv1 host=we8105desk 
| top limit=20 src_ip
```
This query searches the botsv1 index from the host `we8105desk` and show the IPs with the highest activity first while limiting to 20 events by source IP `src_ip`.

<img width="1607" height="159" alt="image" src="https://github.com/user-attachments/assets/f0266378-5588-44c8-b00e-c20a4a686f60" />

- The search returned all sourced IP address related to the host name `we8105desk`. Among all the IP address, `192.168.250.100` has an overwhelming majority of the events (53,106). This is suggest that the IP address of we8105desk (Bob Smith's machine) is associated with `192.168.250.100`.

*Answer: 192.168.250.100*

---

**Question 2: Amongst the Suricata signatures that detected the Cerber malware, which one alerted the fewest number of times? Submit ONLY the signature ID value as the answer.**

Because this is a potential malware execution that could lead to ransomware, I assumed that I did not know the identified Cerber malware, as would be the case in a real investigation. Therefore, I used `suricata`, one of the source types that detects suspicious or anomalous activity, such as malware. This was to confirm whether any related malware had been executed within this timeframe (08/24/2016).

```
index=botsv1 sourcetype=suricata earliest="08/24/2016:00:00:00" latest="08/25/2016:00:00:00"
| stats count by alert.signature
| sort count
```
This query counts and sorts all Suricata alert signatures found in the `botsv1` dataset during August 24–25, 2016, grouped by signature type.

<img width="952" height="583" alt="image" src="https://github.com/user-attachments/assets/0c3d45ea-3016-48e1-b42c-0f119d4bd646" />

- The search returned all alert from `suricata` within the given time frame. The red box highlights the alert triggered by the ransomware, indicating that "**Cerber**" is the detected malware.

Going back to the question, "Cerber" is the identified malware, but we need to submit ONLY the signature that has a fewest number. 

The following is my spl querry I used.

```
index=botsv1 sourcetype=suricata "Cerber" OR "cerber"
| stats count by alert.signature alert.signature_id
```
This query searches Suricata alerts in the `botsv1` dataset for entries containing “Cerber”, then produces a count of each unique alert signature along with its signature ID.

<img width="1912" height="506" alt="image" src="https://github.com/user-attachments/assets/e0a4081e-70de-4b97-bb65-03bc36aa2eca" />

- The search returned all alerts identified as **Cerber**. The signature with the fewest occurrences is `2816763`. This might indicate a successful malware execution because more than one occurrence could represent repeated alerts or failed attempts, while a count of **1** could indicate a successful execution.

*Answer: 2816763*

---

**Question 3: What fully qualified domain name (FQDN) does the Cerber ransomware attempt to direct the user to at the end of its encryption phase?**

To identify the domain name , I need to find first the IP address of Cerber ransomware.

I use this following spl query to find the IP address of Cerber ransomware using the infected host `192.168.250.100` of we8105desk (Bob device).

```
index=botsv1 sourcetype=suricata earliest="08/24/2016:00:00:00" latest="08/25/2016:00:00:00" alert.signature="*Cerber*"
| table _time alert.signature src_ip dest_ip
| sort _time
```

This query retrieves all Suricata alerts in the `botsv1` dataset between August 24–25, 2016 that match _Cerber_, then displays a table of the timestamp, signature, source IP, and destination IP, sorted chronologically.

<img width="1890" height="449" alt="image" src="https://github.com/user-attachments/assets/309ebe98-243f-486b-be01-58e8f1744eac" />

- The search result shows that the Cerber ransomware has already been executed and initiating outbound connections with an external server using the infected host `192.168.250.100`. 
- On August 24, 2016, when the incident happened and from the result, it indicates that Cerber attempts to contact its command-and-control (C2) infrastructure but fail twice at 16:49 to established connections. At 15:12, Cerber performs a new one with the uses of Tor `.onion` domain lookups. These events provide strong evidence that Cerber was active on the infected workstation during the investigation timeframe. 

- The result also found that the infected host address is successfully establish a network connection with this malicious IP address  `192.168.250.20`.

To find the domain name of  Cerber ransomware, I used the malicious IP address and specific time it established a connection (08/24/2016:17:15:12) with the following spl query:

```
index=botsv1 sourcetype=stream:dns earliest="08/24/2016:17:15:12" latest="08/24/2016:17:15:13" src_ip=192.168.250.100 dest_ip=192.168.250.20
| table _time src_ip dest_ip query
```

This query pulls DNS stream logs from the `botsv1` dataset within the one‑second window of **August 24, 2016, 17:15:12–17:15:13**, filtered for traffic between source IP `192.168.250.100` and destination IP `192.168.250.20`, then displays a table of the timestamp, source, destination, and DNS query values.

<img width="1649" height="92" alt="image" src="https://github.com/user-attachments/assets/fa2660da-7019-49cf-a354-1b8e236387c2" />

- From the search result, the domain name Cerber ransomware is the `cerberhhyed5frqa.xmfir0.win`. I can confirm this is the right answer because of the date and time (2016-08-24 17:15:12.668) it occurs exactly from previous result.

*Answer: cerberhhyed5frqa.xmfir0.win*

---

**Question 4: What was the first suspicious domain visited by we8105desk on 24AUG2016?**

`botsv1` has many source type available.  In this part, I will use the HTTP server to find the first domain visited by the host `we8105desk` using the following spl query.

```
index=botsv1 sourcetype=stream:http earliest="08/24/2016:00:00:00" latest="08/25/2016:00:00:00" src_ip=192.168.250.100
| rename site AS domain_name
| table _time dest_ip domain_name 
| dedup domain_name
| sort _time
```

This query retrieves HTTP stream logs from the `botsv1` dataset between August 24–25, 2016 for traffic originating from source IP `192.168.250.100`, renames the `site` field to `domain_name`. Then outputs a table of timestamp, destination IP, and domain name, ensuring each domain appears only once and is sorted chronologically (old to latest).

<img width="1502" height="492" alt="image" src="https://github.com/user-attachments/assets/54fe8f41-4ccf-4fe2-a7a4-d7f4ac4150d2" />

- Based on the search results, the first suspicious domain visited by the host `we8105desk` on **August 24, 2016** at 16:48 UTC, was `solidaritedeproximite.org`.

*Answer: solidaritedeproximite.org*

---
**Question 5: During the initial Cerber infection a VB script is run. The entire script from this execution, pre-pended by the name of the launching .exe, can be found in a field in Splunk. What is the length of the value of this field?**

By searching Sysmon process creation events `sourcetype="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational"` for executables, then calculating the length of that field and sorting to find the longest one we can find the right answer.

```
index=botsv1 host=we8105desk sourcetype="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" EventCode=1 earliest="08/24/2016:00:00:00" latest="08/25/2016:00:00:00" 
| search CommandLine=*vbs* 
| table _time Image CommandLine
```

This sply query results a `.exe` (likely `cscript.exe` or `wscript.exe`) is launching a `.vbs` file. I use this next spl querry to pull all process creation command lines for that day on that host:

```
index=botsv1 host=we8105desk sourcetype="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" EventCode=1 earliest="08/24/2016:00:00:00" latest="08/25/2016:00:00:00"
| table _time CommandLine
```

The question tells us the VBScript's full text is prepended to the launching `.exe` name _inside_ the `CommandLine` field. So this field will contain an unusually long string, not a normal one-line command. I use this next spl query to measure field length and sort to find the longest one.

```
index=botsv1 sourcetype="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" EventCode=1 *.exe CommandLine=* earliest="08/24/2016:00:00:00" latest="08/25/2016:00:00:00"
| eval length=len(CommandLine)
| table CommandLine length
| sort -length
```


<img width="1911" height="261" alt="image" src="https://github.com/user-attachments/assets/5e91b6b1-b40c-472f-86de-f764cf58dce4" />

- From the search result, the top row (longest `CommandLine` value) has `length=4490` that's the launching `.exe` name plus the entire embedded VBScript body, confirming this is the initial Cerber dropper stage.

*Answer: 4490*

----

**Question 6: What is the name of the USB key inserted by Bob Smith?**


To identify the USB, we should know where USB device info lives in Windows. In this case, I use the available source type `WinRegistry` or Window registry logs and search `FriendlyName` keys where windows stores connected hardware data. In Splunk, the `FriendlyName` field from the Windows registry is used to translate cryptic hardware identifiers into human-readable USB device names.

The following spl query I used:

```
index=botsv1 host=we8105desk sourcetype=WinRegistry earliest="08/24/2016:00:00:00" latest="08/25/2016:00:00:00" Friendlyname
| top limit=1 registry_value_data
```

This SPL query searches the `botsv1` index for Windows Registry events from infected host `we8105desk` between August 24–25, 2016 that contain the field `Friendlyname`. It then returns the single most frequent value of `registry_value_data` within those results, along with its count and percentage.

<img width="540" height="201" alt="image" src="https://github.com/user-attachments/assets/825ac6dc-8946-4056-9c08-727204703957" />

- The result show that `MIRANDA_PRI` is the name of the USB key inserted by Bob Smith.

*Answer: MIRANDA_PRI*

---

**Question 7: Bob Smith's workstation (we8105desk) was connected to a file server during the ransomware outbreak. What is the IPv4 address of the file server?**

During Question 3, I had already identified the relevant IPv4 addresses associated with the Cerber ransomware activity by using the following SPL query. The results show both the infected workstation and the destination system, which was later identified as the file server (`192.168.250.20`).

```
index=botsv1 host=we8105desk direction=outbound dest="*we*srv*" earliest="08/24/2016:00:00:00" latest="08/25/2016:00:00:00" 
| sort _time
```

<img width="1864" height="266" alt="image" src="https://github.com/user-attachments/assets/c213fbf1-c0a6-411c-a813-928f38fc7d43" />

- The search results show several Suricata alerts associated with **Cerber ransomware**. The first alerts indicate that the infected workstation attempted to communicate with external command-and-control (C2) infrastructure, followed by **ICMP response errors**, suggesting that some communication attempts were unsuccessful.

- At **17:15:12**, Suricata detected two **Cerber Onion Domain Lookup** alerts. These events indicate that the infected workstation attempted to resolve a Tor (`.onion`) domain, a common technique used by Cerber ransomware to communicate with its infrastructure or direct victims to the ransom payment site.

In the highlighted events:

- **Blue Box (`192.168.250.100`)** — This is the **source IP address**, representing Bob Smith's infected workstation (`we8105desk`), which initiated the network communication.
- **Red Box (`192.168.250.20`)** — This is the **destination IP address**. During the investigation, this address was identified as the **internal file server** that Bob Smith's workstation was connected to during the ransomware outbreak.

Based on these findings, the IPv4 address of the file server is **`192.168.250.20`**.

*Answer: 192.168.250.20*

---

**Question 8: How many distinct PDFs did the ransomware encrypt on the remote file server?**

To identy how many pdf has been encrypted, lets confirm first the file server host as the remote server Bob's machine connected to. 

```
index=botsv1 host=we8105desk direction=outbound dest="*we*srv*" earliest="08/24/2016:00:00:00" latest="08/25/2016:00:00:00" 
| table dest dest_ip src_ip
```

<img width="1435" height="524" alt="image" src="https://github.com/user-attachments/assets/7d20cbaa-96a3-4324-913e-1e41960a9d46" />

- From the result, it appears that the host machine of the IP address `192.168.250.20` is `we9041srv` because it is connected to the infected IP address (Bob's machine). 

Next, I use a different source type `WinEventLog:Security` suit for finding file server and the `host=we9041srv` we recently found.

This spl query was used to find a field name containing all pdf file:

```
index=botsv1 sourcetype="WinEventLog:Security" host=we9041srv earliest="08/24/2016:00:00:00" latest="08/25/2016:00:00:00" "*.pdf"
```

<img width="1127" height="690" alt="image" src="https://github.com/user-attachments/assets/3fb7aece-3e2e-4b67-b675-88f02e29c08f" />

- From the search results, the `Relative_Target_Name` field lists all the PDF files affected by the ransomware.

Then, the `dc` or the distinct count I used to filter out unique files rather than total access events like `stats count`. 

```
index=botsv1 sourcetype="WinEventLog:Security" host=we9041srv earliest="08/24/2016:00:00:00" latest="08/25/2016:00:00:00" "*.pdf"
| stats dc(Relative_Target_Name) as TotalPDFCount
```

However, the result is not the right answer. I tried to remove any duplication in the `Relative_Target_Name` and add another search query defining the source IP address of Bob device using the following SPL query.

```
index=botsv1 sourcetype="WinEventLog:Security" host=we9041srv earliest="08/24/2016:00:00:00" latest="08/25/2016:00:00:00" "*.pdf" Source_Address="192.168.250.100"
| dedup Relative_Target_Name
| stats count
```

<img width="604" height="410" alt="image" src="https://github.com/user-attachments/assets/27c28a07-ff9e-46cf-a086-45fb2b6eb858" />

- The result shows that 257 PDF files were likely encrypted.

*Answer: 257*

---

**Question 9: The VBscript found in question 204 launches 121214.tmp. What is the ParentProcessId of this initial launch?**

Previously from question 5, during the initial Cerber infection a VB script is run. Using the query before, I add some refinement following this spl commands to find the ParentProcessId.

```
index=botsv1 host=we8105desk sourcetype="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" EventCode=1 earliest="08/24/2016:00:00:00" latest="08/25/2016:00:00:00" "121214.tmp" "vbs"
|  table _time parent_process_id
|  dedup parent_process_id
|  sort _time
```

This query searches Sysmon EventCode 1 logs (process creation) between August 24–25, 2016 for processes involving `121214.tmp` and `vbs`, then outputs the event time and parent process ID. It removes duplicate parent process IDs and sorts the results chronologically to show unique parent processes that executed those files.

<img width="1901" height="122" alt="image" src="https://github.com/user-attachments/assets/7445fb64-572f-4c75-b226-0dad663ea26b" />

- The result shows on August 24, 2016, at 16:48 UTC, the `ParentProcessId` of this initial launch is `3968`.

*Answer: 3968*

---

**Question 10: The Cerber ransomware encrypts files located in Bob Smith's Windows profile. How many .txt files does it encrypt?**

 Cerber touches `.txt` files elsewhere on the Windows system folder, but the question specifically asks about files in **Bob's profile**.
 
 The following spl query was used to filter out in Bob windows to located all files `.txt`.


```
index=botsv1 sourcetype="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" host=we8105desk  earliest="08/24/2016:00:00:00" latest="08/25/2016:00:00:00" "*.txt" file_path="C:\\Users\\bob.smith.WAYNECORPINC\\*"
| dedup TargetFilename
| stats count
```

This query searches Sysmon logs on host we8105desk between August 24–25, 2016 for any .txt files accessed under Bob Smith’s user directory. It then deduplicates results by TargetFilename and counts them, effectively showing how many unique text files were touched in that time window.

The `C:\Users\bob.smith.WAYNECORPINC\*` is a Windows file path pointing to the home directory of the user account **bob.smith.WAYNECORPINC**. 

<img width="268" height="107" alt="image" src="https://github.com/user-attachments/assets/97a7fc3f-41c0-4ea5-bd33-02372d110dfe" />

- From the search result, the total .txt files possible encrypt by the Cerber ransomare is `406`

*Answer: 406*


---

**Question 11: The malware downloads a file that contains the Cerber ransomware cryptor code. What is the name of that file?**

Since, I already identified `solidaritedeproximite.org` at suricata's as the first suspicious domain, we will use the source type to filtering parsed HTTP fields down to that host to confirms the exact file requested.

The following spl query I used:

```
index=botsv1 sourcetype=suricata "http.hostname"="solidaritedeproximite.org"
| table http.url
```

This Splunk query looks at Suricata logs for traffic where the HTTP hostname is **solidaritedeproximite.org**. It then extracts and displays the `http.url` field, giving you a list of URLs requested from that domain during the specified time window.

<img width="261" height="253" alt="image" src="https://github.com/user-attachments/assets/bc338186-f745-437f-bf2d-0e36c96eb272" />

- From the result the name of a file that contains the Cerber ransomware cryptor code is `mhtr.jpg`

Answer: mhtr.jpg


---

**Question 12: Now that you know the name of the ransomware's encryptor file, what obfuscation technique does it likely use?**

The ransomware encryptor was disguised with a **`.jpg` file extension**, making it appear to be a legitimate image file. However, instead of containing image data, the file carried malicious executable content.

This behavior is a strong indicator of **steganography**, an obfuscation technique in which malicious code or data is concealed within a file that appears to be harmless. By disguising the malware as a normal image, attackers increase the likelihood that users will open the file while reducing suspicion and potentially bypassing basic security controls.

In this case, the `.jpg` extension was used to **hide the ransomware payload behind the appearance of a legitimate image file**, making **steganography** the most likely obfuscation technique.

*Answer: steganography*


----

**Thankyou for reading this complete walkthrough!**

I hope this investigation demonstrate not only the final answers, but also the analytical process, SPL queries I used, and reasoning to investigate a real-world web defacement incident. My goal in this home lab was to document my learning journey while approaching the scenario from the perspective of a SOC analyst.
