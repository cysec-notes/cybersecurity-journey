# Module 2: Network Operations
## Overview
You will explore network protocols and how network communication can introduce vulnerabilities. In addition, you'll learn about common security measures, like firewalls, that help network operations remain safe and reliable.

## Learning Objectives
After completing this module, I can learn about:
- Network Protovol
- Virtual Private Network (VPNs)
- Firewalls, security zones, & proxy server
  
## Key Concepts Learned
1. **Network protocols** are a set of rules used by two or more devices on a network to describe the order of delivery and the structure of the data.
2. **TCP** is an internet communications protocol that allows two devices (multiple) to form a connection and stream data.
3. The **Address Resolution Protocol**, or ARP, is used to determine the MAC address of the next router or device on the path.
4. The **Hypertext Transfer Protocol Secure**, or HTTPS, is a network protocol that provides a secure method of communication between client and website servers.
5. **Domain Name System**, or DNS, which is a network protocol that translate internet domain names into IP addresses.
  - So just by visiting one website, the device on your networks are using four different protocols: TCP, ARP, HTTPS, and DNS.
6. **IEEE802.11**, commonly known as Wi-Fi, is a set of standards that define communications for wireless LANs.
7. **WPA** is a wireless security protocol for devices to connect to the internet.
8. A **firewall** is a network security device that monitors traffic to and from your network.
9. A firewall can use **port filtering**, which blocks or allows certain port numbers to limit unwanted communication.
10. **Stateful** refers to a class of firewall that keeps track of information passing through it and proactively filters out threats.
11. **Stateless** refers to a class of firewall that operates based on predefined rules and does not keep track of information from data packets.
12. **Encapsulation** is a process performed by a VPN service that protects your data by wrapping sensitive data in other data packets.
    Please note that most websites today use HTTPS. This encrypts the data being transferred between your device and the website. This makes it harder to intercept personal information even if internet traffic can be seen. A VPN encrypts all your internet traffic which helps protect your privacy.
12. A **virtual private network,** also known as a **VPN**, is a network security service that changes your public IP address and hides  your virtual location so that you can keep your data private when you're using a public.
13. **Security zones** are a segment of a network that protects the internal network from the internet. They are a part of a security technique called **network segmentation** that divides the network into segments.
    2 types of security zone:
    1. uncontrolled zone, which is any network outside of the organization's control, like the internet.
    2. controlled zone, which is a subnet that protects the internal network from the uncontrolled zone.
14. **proxy server** is a server that fulfills the request of a client by forwarding them on to other servers.
    Different kinds of proxy:
    - A **forward proxy server** regulates and restricts a person with access to the internet.
    - A **reverse proxy server** regulates and restricts the internet access to an internal server.
    
#### Why learning protocol is important as a SOC analyst?
Understunding how protocol on network is essential as a soc anayst because  they provide structure, consistency, and reliability in handling security incidents. Without clear protocols, analysts risk missing threats, duplicating work, or responding incorrectly.

-  Cybersecurity analysts can leverage their knowledge of protocols to successfully mitigate vulnerabilities on a network and potentially prevent future attacks.
-  Subnetting allows organizations to create smaller networks within their private network. This improves the efficiency of the network and can be used to create security zones.
-  proxy is important
-  Firewall is filtering traffic by ingoing and outgoing traffic and staying alert to network.
-  Network security zones is important where it add a layer of protection from unsecured public external network that we know internet. Ex: firewalls, proxy, IPS/IDS
-  VPN protocols is uesd to encrpted data by encapsulating sensitive information into data packets. It's hide your real ip address and location by the vpn server.
- 

## Next Steps
Continue Course 1 Module 2

NOTE: LEARN Networking
PROXY SEVER, KINDS OF PROXY, SECURITY ZONES. practice cidr/subnetting math.
