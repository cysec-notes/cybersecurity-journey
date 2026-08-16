# Module 4: Vulnerabilities in systems
## Overview

## Learning Objectives
- Exploring **social engineering** tactics, a psychological tricks that attackers use to gain unauthorized access to assets.
- Common type of threat that's been around since the start of personal computers, **malware**.
- Web-based exploits.
- Exploring the threat modeling process.

## Key Concepts I Learned
Social engineering is a manipulation technique that exploits human error to gain private information, access, or valuables.

#### stage of social engineering
1. prepare
2. establish trust
3. Use persuasion tactics
4. Disconnect from target

#### Preventing Social Engineering
- **Implementing managerial controls** like policies, standards, and procedures, are one of the first lines of defense.
- Staying in trend
- User awareness

#### Common types of social engineering
1. **Baiting** is a social engineering tactic that tempts people into compromising their security. A common example is USB baiting that relies on someone finding an infected USB drive and plugging it into their device.
2. **Phishing** is the use of digital communications to trick people into revealing sensitive data or deploying malicious software.
3. **Quid pro quo** is a type of baiting used to trick someone into believing that they’ll be rewarded in return for sharing access, information, or money. 
4. **Tailgating** is a social engineering tactic in which unauthorized people follow an authorized person into a restricted area.
5. **Watering hole** is a type of attack when a threat actor compromises a website frequently visited by a specific group of users. 

A phishing kit is a collection of software tools needed to launch a phishing campaign.

#### Types of Phishing
- **Smishing** is the use of text messages to obtain sensitive information or to impersonate a known source.
- **Vishing** is the exploitation of electronic voice communication to obtain sensitive information or impersonate a known source.
- **Spear phishing** is a subset of email phishing in which specific people are purposefully targeted, such as the accountants of a small business.
- **Whaling** refers to a category of spear phishing attempts that are aimed at high-ranking executives in an organization.

[Practice Phishing attacks attempt](https://phishingquiz.withgoogle.com/)

### Type of Malware
1. Virus - is malicious code written to interfere with computer operations and cause damage to data and software.
2. Worm - is malware that can duplicate and spread itself across systems on its own.
3. trojan - is malware that looks like a legitimate file or program.
4. ransomware - is a type of malicious attack where attackers encrypt an organization's data and demand payment to restore access.
5. spyware - is malware that's used to gather and sell information without consent.
6. scareware - type of malware employs tactics to frighten users into infecting their own device. Scareware tricks users by displaying fake warnings that appear to come from legitimate companies.
7. Fileless malware does not need to be installed by the user because it uses legitimate programs that are already installed to infect a computer.
8. A rootkit is malware that provides remote, administrative access to a computer.
   - A dropper is a type of malware that comes packed with malicious code which is delivered and installed onto a target system.
   - A loader is a type of malware that downloads strains of malicious code from an external source and installs them onto a target system.
9. botnet, short for “robot network,” is a collection of computers infected by malware that are under the control of a single threat actor, known as the “bot-herder.”
10. Cryptojacking is a form of malware that installs software to illegally mine cryptocurrencies.

[One place to learn more about malware analysis is](https://www.infosecinstitute.com/skills/courses/malware-analysis-introduction/) 

#### Web-based exploits
Web-based exploits are malicious code or behavior that's used to take advantage of coding flaws in a web application.

An injection attack is malicious code inserted into a vulnerable application.

A **Cross site scripting**, or XSS, is an injection attack that inserts code into a vulnerable website or web application. These attacks are often delivered by exploiting the two languages used by most websites, HTML and JavaScript. Three main types of cross-site scripting attacks: reflected, stored, and DOM-based.
- A **reflected XSS attack** is an instance where a malicious script is sent to the server and activated during the server's response.
- A **stored XSS attack** is an instance when malicious script is injected directly on the server.
- A **DOM-based XSS attack** is an instance when malicious script exists in the web page a browser loads.

A SQL injection is an attack that executes unexpected queries on a database.

#### Injection Prevention
- A **prepared statement** is a coding technique that executes SQL statements before passing them on to the database.
- Input sanitization: programming that removes user input which could be interpreted as code.
- Input validation: programming that ensures user input meets a system's expectations.

[OWASP's SQL injection detection techniques](https://owasp.org/www-project-web-security-testing-guide/latest/4-Web_Application_Security_Testing/07-Input_Validation_Testing/05-Testing_for_SQL_Injection) is a useful resource if you're interested in investigating SQL injection vulnerabilities on your own.

#### A proactive approach to security
**Threat modeling** is a process of identifying assets, their vulnerabilities, and how each is exposed to threats. Threat Modeling steps:
- Define the scope
- Identify threats. An attack tree is a diagram that maps threats to assets.
-  characterize the environment.
-  analyze threats
-  mitigate risk
-  evaluate findings

PASTA is a popular threat modeling framework that's used across many industries.


## Personal reflection and Key takeaways
- 





