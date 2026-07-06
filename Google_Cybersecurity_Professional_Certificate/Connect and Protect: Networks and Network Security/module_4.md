# Module 4: Security Hardening
## Overview
You will become familiar with network hardening practices that strengthen network systems. You'll learn how security hardening helps defend against malicious actors and intrusion methods. You'll also learn how to use security hardening to address the unique security challenges posed by cloud infrastructures.

After completing this module, I can:
- Security hardening
- OS hardening
- Explore network harding practices
- Cloud network hardening

## Key Concepts Learned
Where Security hardening occur?
  - Networks
  - Devices
  - Applications
  - Cloud infastructure
 
  Security Analyst responsibilities in Security Hardening
  - patch updates
  - backups
    
1. **Security hardening** is the process of strengthening a system to reduce its vulnerability and attack surface.
2. **Attack surface** - All the potential vulnerabilities that a threat actor could exploit are referred to as a system's attack surface.

Security Hardening can be conducted on
- Hardware
- Operating System
- Applications
- Computer networks
- Databases

3. A **penetration test**, also called a pen test, is a simulated attack that helps identify vulnerabilities in a system, network, website, application, and process.

#### OS Hardening
The **operating system** is the interface between computer hardware and the user.

A **patch update** is a software and operating system, or OS, update that addresses security vulnerabilities within a program or product.
A **baseline configuration** is a documented set of specifications within a system that is used as a basis for future builds, releases, and updates.
**MFA** is a security measure which requires a user to verify their identity in two or more ways to access a system or network.

#### Brute force attacks and OS hardening
A **brute force attack** is a trial-and-error process of discovering private information. 

Different types of brute force attacks that malicious actors use to guess passwords, including: 
1. **Simple brute force attacks**. When attackers try to guess a user's login credentials, it’s considered a simple brute force attack. They might do this by entering any combination of usernames and passwords that they can think of until they find the one that works.
2. **Dictionary attacks** use a similar technique. In dictionary attacks, attackers use a list of commonly used passwords and stolen credentials from previous breaches to access a system. These are called “dictionary” attacks because attackers originally used a list of words from the dictionary to guess the passwords, before complex password rules became a common security practice. 

To protect against brute force attacks, cybersecurity analysts can use sandboxes to test suspicious files, check for vulnerabilities, or to simulate real attacks and virtual machines to conduct vulnerability tests. Some common measures to prevent brute force attacks include: hashing and salting, MFA and/or 2FA, CAPTCHA and reCAPTCHA, and password policies.

Some of the common security methods used to prevent brute force attacks include:
- Requiring strong passwords
- Enforcing two-factor authentication (2FA)
- Monitoring login attempts
- Requiring more frequent password changes
- Disallowing previous passwords from being used
- Limiting the number of login attempts

### Network hardening practices
- Port filtering
- Network Access Priveledge
- Encryption

Network log analysis is the process of examining network logs to identify events of interest.

A SIEM tool is an application that collects and analyzes log data to monitor critical activities in an organization.

Port filtering is a firewall function that blocks or allows certain port numbers to limit unwanted communication.

Firewall rules maintenance: 
Network log analysis:
Network segmentation: 
Encryption

An intrusion detection system (IDS) is an application that monitors system activity and alerts on possible intrusions.

An intrusion prevention system (IPS) is an application that monitors system activity for intrusive activity and takes action to stop the activity. It offers even more protection than an IDS because it actively stops anomalies when they are detected, unlike the IDS that simply reports the anomaly to a network administrator.

### Cloud Network
A **cloud network** is a collection of servers or computers that stores resources and data in a remote data center that can be accessed via the internet.

Identity access management (IAM) is a collection of processes and technologies that helps organizations manage digital identities in their environment. 


## Personal Reflection
Examples of security hardening installing cctv, update patches, ensure encryption, conduct regualr penetration testing, strong password policy, 
As a security analyst, you may be responsible for initiating network security practices. Making executive decisions about which tools to use based on what you know about certain vulnerabilities will be a starting point for helping the organization improve its network security. Explaining and documenting your decisions as a cybersecurity analyst will help in the future if the network ever needs to be troubleshooted. It will also help give non-technical employees buy-in and help them follow security practices, such as multifactor authentication. 

Some common cloud security hardening techniques
1. Identity access management (IAM) is a collection of processes and technologies that helps organizations manage digital identities in their environment. This service also authorizes how users can leverage different cloud resources.
2. Hypervisor abstracts the host’s hardware from the operating software environment. There are two types of hypervisors. Type one hypervisors run on the hardware of the host computer. Type two hypervisors operate on the software of the host computer
3. Baselining for cloud networks and operations cover how the cloud environment is configured and set up.
4. Cryptography can be applied to secure data that is processed and stored in a cloud environment. Cryptography uses encryption and secure key management systems to provide data integrity and confidentiality. Cryptographic encryption is one of the key ways to secure sensitive data and information in the cloud.
5. Cryptographic erasure is a method of erasing the encryption key for the encrypted data. When destroying data in the cloud, more traditional methods of data destruction are not as effective. Crypto-shredding is a newer technique where the cryptographic keys used for decrypting the data are destroyed.



## Next Steps
Continue Course 1 Module 2


