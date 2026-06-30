# Module 1: Network Architecture
## Overview
You'll be introduced to network security and explain how it relates to ongoing security threats and vulnerabilities. You will learn about network architecture and mechanisms to secure a network.

## Learning Objectives
After completing this module, I can:
- Structured of a Network
- Standard Networking Tools
- Cloud Networks
- TCP/IP Model

## Key Concepts Learned
#### What is Network?
- A network is a group of connected devices. Devices can communicate on two types of networks: a local area network, also known as a **LAN**, and a wide area network, also known as a **WAN**.

A local area network, or LAN, spans a small area like an office building, a school, or a home.
Wide are network, or Wan, a network that span a geographic area like a city, state, country

#### Network tools
1. Hub - is a network device that broadcasts information to every device on the network.
2. Switch - makes connections between specific devices on a network by sending and receiving data between them.
3. Router - is a network device that connects multiple networks together.
4. Modem - is a device that connects your router to the internet, and brings internet access to the LAN.

**Firewalls** -  is a network security device that monitors traffic to or from your network. It is like your first line of defense. **Servers** provide information and services for devices like computers, smart home devices, and smartphones on the network. 

**Cloud computing** is the practice of using remote servers, applications, and network services that are hosted on the internet instead of on local physical devices.  A **cloud network** is a collection of servers or computers that stores resources and data in a remote data center that can be accessed via the internet.

A **data packet** is a basic unit of information that travels from one device to another within a network. The movement of data packets across a network can provide an indication of how well the network is performing. Network performance can be measured by **bandwidth**. Bandwidth refers to the amount of data a device receives every second. You can calculate bandwidth by dividing the quantity of data by the time in seconds. **Speed** refers to the rate at which data packets are received or downloaded.

**Packet sniffing** is the practice of capturing and inspecting data packets across the network.
a **Port** is a software-based location that organizes the sending and receiving of data between devices on a network.
#### TCP/IP Model 
First, TCP, or Transmission Control Protocol, is an internet communication protocol that allows two devices to form a connection and stream data. The IP in TCP/IP stands for Internet Protocol. IP has a set of standards used for routing and addressing data packets as they travel between devices on a network.

The TCP/IP model is a framework used to visualize how data is organized and transmitted across a network. 

<img width="643" height="451" alt="image" src="https://github.com/user-attachments/assets/3d5f650d-cd37-4f6b-ada3-7eb6104cd200" />

1. Network access layer - sometimes called the data link layer, deals with the creation of data packets and their transmission across a network
2. The internet layer, sometimes referred to as the network layer, is responsible for ensuring the delivery to the destination host, which potentially resides on a different network.
   **Internet Protocol (IP)**. IP sends the data packets to the correct destination and relies on the **Transmission Control Protocol/User Datagram Protocol (TCP/UDP)**
   **Internet Control Message Protocol (ICMP).** The ICMP shares error information and status updates of data packets. This is useful for detecting and troubleshooting network errors.
3. The transport layer is responsible for delivering data between two systems or networks and includes protocols to control the flow of traffic across a network. TCP and UDP are the two transport protocols that occur at this layer.
    **Transmission Control Protocol (TCP)** - It ensures that data is **reliably** transmitted to the destination service
   **User Datagram Protocol (UDP)** - is a connectionless protocol that does not establish a connection between devices before transmissions. It is used by applications that are not concerned with the reliability of the transmission.
4. Application layer - The application layer in the TCP/IP model is similar to the application, presentation, and session layers of the OSI model. The application layer is responsible for making network requests or responding to requests.
   This layer defines which internet services and applications any user can access. Protocols in the application layer determine how the data packets will interact with receiving devices. Some common protocols used on this layer are: 
  - Hypertext transfer protocol (HTTP)
  - Simple mail transfer protocol (SMTP)
  - Secure shell (SSH)
  - File transfer protocol (FTP)
  - Domain name system (DNS)

<img width="1011" height="492" alt="image" src="https://github.com/user-attachments/assets/ae5fe680-e144-45fa-8bf0-7e62d8a2fea2" />
The TCP/IP model is a simplified version of the OSI model.

An **internet protocol address**, or **IP address**, is a unique string of characters that identifies a location of a device on the internet.
-  IPv4, and IPv6.

A MAC address is a unique alphanumeric identifier that is assigned to each physical device on a network.

## Skills Gained

## Personal Reflection
- In this reading, I learned more about cloud computing and cloud networking. I learned that CSPs are companies that own large data centers that house millions of servers in locations all over the globe and then provide modern technology services, including compute, storage, and networking, through the internet. SDNs are an approach to network management. SDNs enable dynamic, programmatically efficient network configurations to improve network performance and monitoring. This makes it more like cloud computing than traditional network management. Organizations can improve reliability, save costs, and scale quickly by using CSPs to provide networking services instead of building and maintaining their own network infrastructure. As a security professional, it's important that understand the TCP/IP model because it describes the functions of various network protocols. Both osi/tcp/ip models help professionals visualize how data transmitted in the network

## Next Steps
Continue Course 1 Module 2


