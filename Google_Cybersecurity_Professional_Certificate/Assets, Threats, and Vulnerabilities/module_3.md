# Module 3: Vulnerabilities in systems
## Overview
In this module, learners will build an understanding of the vulnerability management process. They will learn about common vulnerabilities . They will develop an attacker mindset by examining the ways vulnerabilities can become threats to asset security if they are exploited.

## Learning Objectives
- Explore a common approach to vulnerability management
- Defense and depth model.
- The CVE list
- Discuss the **attack surfaces** security teams protect.
- Expand your attacker mindset by exploring the common **attack vectors** cybercriminals try to exploit.
  
## Key Concepts I Learned
In security, an **exploit** is a way of taking advantage of a vulnerability.

**Vulnerability management** is the process of finding and patching vulnerabilities.

4 Steps process of Vulnerability Management
- Identify vulnerabilities
- Consider potential exploit
- Prepare defense against threat
- Evaluate those defenses

A **zero-day** is an exploit that was previously unknown.

**Continuous Delivery, and Continuous Deployment** (CI/CD) - automates the entire software release process, from code creation to deployment. 
**Continuous Integration (CI)** is all about frequently merging code changes from different developers into a central location.
**Continuous Delivery: Ready to Release** -  means your code is always ready to be released to users.
**Continuous Deployment (CD): Fully Automated Releases** - automates the entire release process. 

#### Defense in depth strategy
Defense in depth - It's a layered approach to vulnerability management that reduces risk.
1. perimeter layer- like usernames and passwords (authentication).
2. network layer - like network firewalls and others (authorization).
3. Endpoints - refer to the devices that have access on a network.
4. Application layer - are used to interact with technology.
5. Data layer - identifiable information (critical data).

#### Common vulnerabilities and exposures
The common vulnerabilities and exposures list, or **CVE** list, is an openly accessible dictionary of known vulnerabilities and exposures. CVE developed by **MITRE**, is a collection of non-profit research and development centers.

A **CNA** (CVE numbering authority) is an organization that volunteers to analyze and distribute information on eligible CVEs.

The **NIST National Vulnerabilities Database** uses what's known as the common vulnerability scoring system, or **CVSS**, which is a measurement system that scores the severity of a vulnerability.

**OWASP** is a nonprofit foundation that works to improve the security of software. OWASP is an open platform that security professionals from around the world use to share information, tools, and events that are focused on securing the web.

**OSINT** is the collection and analysis of information from publicly available sources to generate usable intelligence. I

A **vulnerability assessment** is the internal review process of an organization's security systems.

A **vulnerability scanner** is software that automatically compares known vulnerabilities and exposures against the technologies on the network. In general, these tools scan systems to find misconfigurations or programming flaws.

**Attack vectors** refer to the pathways attackers use to penetrate security defenses.


## Portfolio Activity: Analyze a vulnerable system for a small business
In this activity, I conduct a [vulnerability assessment](Portfolio-Vulnerability_Assessment_Report.pdf) for a small business. I will evaluate the risks of a vulnerable information system and outline a remediation plan.

**Scenario:**
You are a newly hired cybersecurity analyst for an e-commerce company. The company stores information on a remote database server, since many of the employees work remotely from locations all around the world. Employees of the company regularly query, or request, data from the server to find potential customers. The database has been open to the public since the company's launch three years ago. As a cybersecurity professional, you recognize that keeping the database server open to the public is a serious vulnerability.

## Activity: Identify the attack vectors of a USB drive
In this activity, I perform this [Parking lot USB exercise](Parking-lot-USB-exercise.pdf) activity to assess the attack vectors of a USB drive. Consider a scenario of finding a USB drive in a parking lot from both the perspective of an attacker and a target.

**Scenario:**
You are part of the security team at Rhetorical Hospital and arrive to work one morning. On the ground of the parking lot, you find a USB stick with the hospital's logo printed on it. There’s no one else around who might have dropped it, so you decide to pick it up out of curiosity. You bring the USB drive back to your office where the team has virtualization software installed on a workstation. Virtualization software can be used for this very purpose because it’s one of the only ways to safely investigate an unfamiliar USB stick. The  software works by running a simulated instance of the computer on the same workstation. This simulation isn’t connected to other files or networks, so the USB drive can’t affect other systems if it happens to be infected with malicious software.


## Personal reflection and Key takeaways
- While a **vulnerability** is a weakness of a system, an **exposure** is a mistake that can be exploited by a threat.
- To prepare for future risks, security professionals need to stay informed.
- Practicing an attacker mindset
  

[Continue Course 5 Module 4](module_4.md)


