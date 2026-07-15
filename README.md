# Netcat (nc) Networking Lab – A Practical Guide to TCP Communication, Service Enumeration, and Network Troubleshooting

> A hands-on networking laboratory demonstrating the practical use of **Netcat (nc)** for TCP communication, file transfer, port scanning, banner grabbing, HTTP protocol testing, and network troubleshooting in a virtualized lab environment.

![Platform](https://img.shields.io/badge/Platform-Kali%20Linux-blue)
![Windows](https://img.shields.io/badge/Windows-11-0078D6)
![Juice Shop](https://img.shields.io/badge/Juice_Shop-17.1.1-F49C12)
![Metasploitable2](https://img.shields.io/badge/Metasploitable2-Lab-red)
![Tool](https://img.shields.io/badge/Tool-Netcat-success)
![Status](https://img.shields.io/badge/Project-Completed-brightgreen)


---

# Project Overview

Netcat (commonly known as **nc**) is one of the most versatile networking utilities available for Linux and Unix-like operating systems. Due to its flexibility in creating, reading, and writing TCP and UDP connections, it is widely recognized as the **"Swiss Army Knife of Networking."**

This project demonstrates the practical use of Netcat in a controlled virtual laboratory environment to understand how TCP communication works at the socket level. Rather than focusing on offensive techniques, the project emphasizes networking fundamentals, service verification, protocol analysis, and troubleshooting skills that are directly applicable to **Security Operations Center (SOC)**, **Blue Team**, **Network Administration**, and **IT Support** roles.

The laboratory exercises cover the complete workflow of establishing TCP connections, transferring files, verifying service availability, identifying network services through banner grabbing, manually interacting with HTTP servers, and troubleshooting connectivity issues using Netcat.

Each phase includes:

- Objective
- Theory
- Commands Executed
- Expected Output
- Actual Output
- Technical Explanation
- Troubleshooting Notes
- Screenshots
- Key Takeaways

---

# Objectives

The primary objectives of this project are to:

- Understand TCP client-server communication.
- Learn how Netcat creates TCP and UDP connections.
- Demonstrate manual file transfer over TCP.
- Perform service verification using Zero-I/O port scanning.
- Identify network services through banner grabbing.
- Manually construct and analyze HTTP requests.
- Develop practical troubleshooting techniques for common network connectivity issues.
- Document each exercise in a professional and reproducible manner suitable for technical portfolios.

---

# Skills Demonstrated

This project demonstrates practical experience with:

- TCP Socket Communication
- Client-Server Architecture
- File Transfer over TCP
- Zero-I/O Port Scanning
- Banner Grabbing
- Service Enumeration
- HTTP Request Construction
- HTTP Response Analysis
- Network Troubleshooting
- Connectivity Verification
- Basic Protocol Analysis
- Technical Documentation
- GitHub Project Documentation

---
## Table of Contents

- [Project Overview](#project-overview)
- [Learning Objectives](#learning-objectives)
- [Key Features](#key-features)
- [Lab Environment](#lab-environment)
- [Network Topology](#network-topology)
- [Repository Structure](#repository-structure)
- [Project Phases](#project-phases)
- [Hands-on Laboratory Exercises](#hands-on-laboratory-exercises)
  - [Phase 1 – TCP Client-Server Communication](#phase-1--tcp-client-server-communication)
  - [Phase 2 – File Transfer Using Netcat](#phase-2--file-transfer-using-netcat)
  - [Phase 3 – Zero-I/O Port Scanning Using Netcat](#phase-3--zero-io-port-scanning-using-netcat)
  - [Phase 4 – Banner Grabbing & Service Enumeration](#phase-4--banner-grabbing--service-enumeration)
  - [Phase 5 – HTTP Request Testing Using Netcat](#phase-5--http-request-testing-using-netcat)
- [Project Summary](#project-summary)
- [Technical Skills Demonstrated](#technical-skills-demonstrated)
- [Key Learning Outcomes](#key-learning-outcomes)
- [Challenges Encountered and Solutions](#challenges-encountered-and-solutions)
- [Practical Applications](#practical-applications)
- [Future Enhancements](#future-enhancements)
- [References](#references)
- [Conclusion](#conclusion)
- [Acknowledgements](#acknowledgements)
- [Connect With Me](#connect-with-me)
---

# Lab Environment

The laboratory was built using a virtualized environment to simulate real-world network communication between multiple systems. Each virtual machine was assigned a specific role to demonstrate practical networking concepts using Netcat.

| Component | Version / Platform | Purpose |
|------------|--------------------|---------|
| Host Operating System | Kali Linux  | Runs Oracle VirtualBox and hosts all virtual machines |
| Oracle VirtualBox | 7.2.12r174389 | Virtualization platform |
| Kali Linux VM | Kali Linux 2026.3 | Primary attacker/client machine used for executing Netcat commands |
| Windows 11 VM | Windows 11 | Listener (server) and client for TCP communication |
| Metasploitable2 | Ubuntu-based Vulnerable VM | Target machine for banner grabbing and service enumeration |
| OWASP Juice Shop | Ubuntu 24.04 | HTTP server used for manual HTTP request testing |
| Netcat | OpenBSD Netcat / Ncat | Networking utility used throughout the project |

---

# Network Topology

The virtual machines communicate using a **Host-Only Network Adapter**, providing an isolated environment for laboratory testing without exposing services to external networks.

```mermaid
  flowchart TD
    subgraph Host-Only Network [Host-Only Network: 192.168.56.0/24]
        Win11["Windows 11<br>(TCP Listener VM)<br>IP: 192.168.56.107"]
        Kali["Kali Linux<br>(Client / Analysis VM)<br>IP: 192.168.56.106"]
        MS2["Metasploitable2<br>(Service Target VM)<br>IP: 192.168.56.101"]
        Juice["OWASP Juice Shop<br>(HTTP Server)<br>IP: 192.168.56.105"]
        
        Switch((Virtual<br>Switch))

        Win11 --- Switch
        Kali --- Switch
        MS2 --- Switch
        Juice --- Switch
    end
```
> **Note:** The IP addresses shown above reflect the lab environment used during this project. Your environment may use different addresses depending on your VirtualBox network configuration.

---

# Repository Structure

The repository is organized to provide a clear separation between documentation, screenshots, and supporting assets used throughout the laboratory exercises.

```text
netcat-networking-lab/
│
├── README.md                          # Complete project documentation
├── .gitignore                         # Git ignore rules
│
├── screenshots/
│   ├── phase-1-tcp-chat/
│   ├── phase-2-file-transfer/
│   ├── phase-3-port-scanning/
│   ├── phase-4-banner-grabbing/
│   ├── phase-5-http-testing/
│   └── phase-6-network-troubleshooting/
```

### Repository Contents

| Item | Description |
|------|-------------|
| **README.md** | Contains the complete project documentation, including theory, lab setup, commands, screenshots, technical explanations, troubleshooting, and conclusions. |
| **LICENSE** | Defines the licensing terms for this project. |
| **.gitignore** | Specifies files and directories that Git should ignore. |
| **screenshots/** | Contains screenshots captured during each phase of the laboratory exercises. |
| **assets/** | Stores diagrams, network topology illustrations, and reference images used throughout the documentation. |

> **Note:** All documentation for this project is intentionally maintained within a single `README.md` file to provide a seamless reading experience. This allows readers to follow the complete lab from start to finish without navigating between multiple documents.

---

# Project Phases

The project is divided into six practical phases, each focusing on a different networking concept.

| Phase | Topic | Skills Demonstrated |
|------:|-------|---------------------|
| 1 | TCP Client-Server Communication | TCP sockets, listeners, clients |
| 2 | File Transfer Using Netcat | File transmission over TCP |
| 3 | Zero-I/O Port Scanning | Service discovery and port verification |
| 4 | Banner Grabbing & Service Enumeration | Protocol identification and service validation |
| 5 | HTTP Request Testing | Manual HTTP communication and response analysis |

| 6 | Network Troubleshooting | Connectivity verification and TCP communication analysis |

---

# Understanding Netcat

Before diving into the hands-on exercises, it is important to understand what **Netcat** is, how it works, and why it is considered one of the most versatile networking utilities available.

## What is Netcat?

**Netcat (nc)** is a lightweight command-line networking utility capable of reading from and writing to network connections using the **Transmission Control Protocol (TCP)** and the **User Datagram Protocol (UDP)**. It allows users to establish direct communication between two systems, making it an invaluable tool for network administrators, security professionals, penetration testers, and developers.

Originally developed by **Hobbit** in 1995, Netcat has become a standard networking utility available on most Linux distributions and is also included with **Nmap** as **Ncat** on Windows.

Unlike traditional networking tools that are designed for a single purpose, Netcat provides multiple networking capabilities through a single executable.

---

## Why is Netcat Called the "Swiss Army Knife of Networking"?

Netcat has earned the nickname **"Swiss Army Knife of Networking"** because a single tool can perform many different networking tasks.

Some of its most common capabilities include:

- Establishing TCP client-server communication
- Transferring files between systems
- Creating TCP and UDP listeners
- Performing basic port scanning
- Verifying service availability
- Banner grabbing and service identification
- Testing HTTP, FTP, SMTP, and other application protocols
- Network troubleshooting and connectivity testing
- Debugging network applications

Rather than installing multiple utilities for each networking task, Netcat provides these capabilities through simple command-line options.

---

## How Netcat Works

Netcat operates at the **Transport Layer (Layer 4)** of the OSI model by creating raw TCP or UDP socket connections.

Depending on how it is executed, Netcat can operate in two modes:

### Client Mode

In client mode, Netcat initiates a connection to a remote host and port.

```
Client (Kali Linux)
        │
        │ TCP Connection Request
        ▼
Server (Windows 11)
```

Example:

```bash
nc 192.168.56.107 4444
```

---

### Listener Mode

In listener mode, Netcat waits for incoming connections from remote systems.

```
Windows 11
Listening on Port 4444
        ▲
        │
Incoming TCP Connection
        │
Kali Linux
```

Example:

```bash
nc -l 4444
```

Once a client connects, both systems can exchange data over the established TCP session.

---

## TCP vs UDP

Netcat supports communication using both TCP and UDP protocols.

| Feature | TCP | UDP |
|----------|-----|-----|
| Connection-Oriented | ✅ Yes | ❌ No |
| Reliable Delivery | ✅ Yes | ❌ No |
| Packet Ordering | ✅ Guaranteed | ❌ Not Guaranteed |
| Error Checking | ✅ Yes | Limited |
| Typical Use Cases | SSH, HTTP, FTP | DNS, DHCP, VoIP, Streaming |

Throughout this project, all exercises use **TCP** because it provides reliable communication and is commonly used by enterprise services.

---

## Common Netcat Options

The following options are used throughout this laboratory.

| Option | Description |
|---------|-------------|
| `-l` | Listen for incoming connections |
| `-v` | Enable verbose output |
| `-z` | Zero-I/O mode (used for port scanning) |
| `-u` | Use UDP instead of TCP |
| `-p` | Specify the local source port |
| `-w` | Set a connection timeout |

---

## Lab Objectives

The practical exercises in this repository are designed to demonstrate how Netcat can be used for common networking tasks in a controlled laboratory environment.

By completing this project, you will learn how to:

- Establish TCP client-server communication.
- Transfer files over a TCP connection.
- Verify service availability using Zero-I/O scanning.
- Identify running services through banner grabbing.
- Manually interact with HTTP servers.
- Troubleshoot TCP connectivity issues.
- Understand how applications communicate over the network.

---
---

# Hands-on Laboratory Exercises

This section documents the practical implementation of Netcat within a controlled virtual laboratory environment. Each phase builds upon the previous one, gradually introducing new networking concepts while reinforcing core TCP communication principles.

Every exercise follows a consistent structure to ensure clarity, reproducibility, and ease of understanding.

Each phase includes:

- **Objective** – The purpose of the exercise.
- **Background Theory** – Fundamental networking concepts related to the activity.
- **Lab Environment** – Virtual machines and services used.
- **Commands Executed** – Complete commands used during the exercise.
- **Command Explanation** – Detailed explanation of each command and its parameters.
- **Expected Results** – The anticipated output before execution.
- **Actual Results** – The observed output captured during the lab.
- **Technical Analysis** – Explanation of what occurred at the protocol and application levels.
- **Screenshots** – Visual evidence of successful execution.
- **Troubleshooting** – Issues encountered and the steps taken to resolve them.
- **Key Takeaways** – Important concepts learned during the exercise.

The laboratory was performed in an isolated VirtualBox Host-Only network using Kali Linux, Windows 11, Metasploitable2, and OWASP Juice Shop. All commands, outputs, and screenshots presented in this repository were generated during the execution of this lab.

---

# Phase 1 – TCP Client-Server Communication

**Objective:** Establish a reliable TCP client-server connection using Netcat to understand socket communication, connection establishment, and bidirectional data exchange.

---

## Quick Summary

| Category | Details |
|----------|---------|
| **Objective** | Establish a TCP client-server connection using Netcat |
| **Protocol** | TCP |
| **Port** | 4444 |
| **Client Machine** | Kali Linux |
| **Listener Machine** | Windows 11 |
| **Tool** | Netcat (nc / Ncat) |
| **Network** | VirtualBox Host-Only Adapter |
| **Estimated Time** | 10–15 Minutes |
| **Difficulty** | Beginner |

---

## Background Theory

The **Transmission Control Protocol (TCP)** is a **connection-oriented** protocol that provides reliable communication between two hosts. Before any application data is transmitted, TCP establishes a connection using the **Three-Way Handshake**, ensuring both systems are ready to communicate.

In this exercise:

- **Windows 11** acts as the **TCP Listener (Server)**.
- **Kali Linux** acts as the **TCP Client**.
- Communication occurs over a VirtualBox **Host-Only Network**, providing an isolated and controlled lab environment.

---

## Network Communication Flow

The following diagram illustrates the communication path between the client and the listener.

```mermaid
flowchart LR

subgraph HostOnly["VirtualBox Host-Only Network (192.168.56.0/24)"]

Kali["💻 Kali Linux<br/>Client<br/>192.168.56.106"]

Windows["🖥️ Windows 11<br/>Listener<br/>192.168.56.107"]

Kali -- "TCP Port 4444" --> Windows

end
```

---

## TCP Three-Way Handshake

Before any data can be exchanged, TCP establishes a reliable connection using the three-way handshake.

```mermaid
sequenceDiagram
    participant C as Kali Linux (Client)
    participant S as Windows 11 (Listener)

    C->>S: SYN
    S->>C: SYN + ACK
    C->>S: ACK

    Note over C,S: TCP Connection Established

    C->>S: Hello from Kali
    S->>C: Hello from Windows
```

---

# Exercise 1.1 – Configure the TCP Listener (Windows 11)

Launch **PowerShell** on the Windows 11 virtual machine and start Netcat in listening mode.

## Command

```powershell
ncat -l 4444
```

### Command Breakdown

| Parameter | Description |
|-----------|-------------|
| `ncat` | Launches the Netcat utility |
| `-l` | Enables Listener Mode |
| `4444` | TCP port used to accept incoming connections |

### Expected Output

```text
PS C:\Users\vboxuser> ncat -l 4444
```

The listener waits silently until a client initiates a connection.

### Evidence

**Figure 1.1 – Windows 11 waiting for incoming TCP connections**

> `screenshots/phase-1/01-listener-started.png`

---

# Exercise 1.2 – Establish the Client Connection (Kali Linux)

From the Kali Linux virtual machine, initiate a TCP connection to the Windows listener.

## Command

```bash
nc -v 192.168.56.107 4444
```

> Replace the IP address if your Windows VM uses a different address.

### Command Breakdown

| Parameter | Description |
|-----------|-------------|
| `nc` | Launches Netcat |
| `-v` | Enables verbose mode |
| `192.168.56.107` | Windows Listener IP Address |
| `4444` | Destination TCP Port |

### Expected Output

```text
Connection to 192.168.56.107 4444 port [tcp/*] succeeded!
```

This confirms:

- The listener is operational.
- The TCP three-way handshake completed successfully.
- A bidirectional communication channel has been established.

### Evidence

**Figure 1.2 – Kali Linux successfully connected to the Windows listener**

> `screenshots/phase-1/02-client-connected.png`

---

# Exercise 1.3 – Verify Bidirectional Communication

After the connection is established, both systems can exchange text messages over the active TCP session.

### Example Communication

After the TCP connection was successfully established, messages were exchanged between the client and the listener to verify bidirectional communication.

**Message sent from Kali Linux (Client):**

```text
Hello Windows!
```

**Message sent from Windows 11 (Listener):**

```text
Hello Kali
```

The successful exchange of messages confirms that:

- The TCP session was established successfully.
- Both systems were able to send and receive data over the same connection.
- Netcat provided full-duplex communication, allowing interactive data exchange between the client and the listener.

### Evidence

**Figure 1.3 – Successful bidirectional communication between Kali Linux and Windows 11**

> `screenshots/phase-1/03-message-exchange.png`
---

## Verification Checklist

The exercise is considered successful when the following conditions are met:

- ✅ Windows entered listening mode successfully.
- ✅ Kali Linux established a TCP connection.
- ✅ The TCP handshake completed successfully.
- ✅ Messages were exchanged in both directions.
- ✅ No connection errors or packet loss were observed.

---

## Technical Analysis

When the client executes:

```bash
nc -v 192.168.56.107 4444
```

the operating system creates a TCP socket and sends a **SYN** packet to the Windows listener. The listener responds with a **SYN-ACK**, indicating that it is ready to establish a connection. Finally, the Kali client replies with an **ACK**, completing the TCP three-way handshake.

Once the connection is established, Netcat redirects the standard input (`stdin`) and standard output (`stdout`) streams through the TCP socket. This allows both systems to exchange data interactively over a reliable transport-layer connection.

TCP ensures:

- Reliable data delivery
- Ordered packet transmission
- Error detection and recovery
- Connection state management

These characteristics make TCP the preferred protocol for services such as SSH, HTTP, FTP, SMTP, and database communication.

---

## Security Perspective

Understanding TCP communication is fundamental for cybersecurity professionals.

SOC analysts routinely investigate TCP sessions while analyzing:

- Unauthorized remote access attempts
- Suspicious outbound connections
- Malware Command-and-Control (C2) traffic
- Lateral movement within enterprise networks
- Firewall and IDS/IPS alerts
- Network service availability issues

A solid understanding of TCP communication enables analysts to interpret packet captures, firewall logs, SIEM events, and network alerts more effectively.

---

## Real-World Applications

The concepts demonstrated in this exercise are directly applicable to enterprise networking environments.

Examples include:

- Remote administration using SSH
- Web communication through HTTP and HTTPS
- Secure file transfers using FTP and SFTP
- Email delivery using SMTP
- Database client-server communication
- Internal application communication
- Network troubleshooting and diagnostics

---

## Troubleshooting

| Issue | Possible Cause | Resolution |
|--------|----------------|------------|
| Connection refused | Listener is not running | Start the Netcat listener before connecting. |
| Connection timed out | Firewall or incorrect IP address | Verify firewall rules and confirm the destination IP address. |
| Host unreachable | Network connectivity issue | Confirm both VMs are connected to the same Host-Only network. |
| Incorrect port | Listener configured on a different port | Ensure the client and listener use the same TCP port. |

---

## Key Takeaways

- Established a reliable TCP client-server connection using Netcat.
- Understood how TCP sockets enable communication between hosts.
- Observed the TCP Three-Way Handshake in a practical scenario.
- Successfully exchanged bidirectional messages over a TCP session.
- Learned how Netcat functions as both a TCP client and a TCP listener.
- Connected networking theory with real-world enterprise communication workflows.
- Built a strong foundation for subsequent Netcat exercises, including file transfer, port scanning, service enumeration, and protocol testing.

---
# Phase 2 – File Transfer Using Netcat

> **Objective:** Transfer a file between two virtual machines using Netcat over a TCP connection and verify its integrity using SHA-256 hashing.

---

## Quick Summary

| Category | Details |
|----------|---------|
| **Objective** | Transfer a file over TCP using Netcat |
| **Protocol** | TCP |
| **Port** | 5555 |
| **Sender** | Kali Linux |
| **Receiver** | Windows 11 |
| **Tool** | Netcat (nc / Ncat) |
| **Verification** | SHA-256 Hash Comparison |
| **Difficulty** | Beginner |
| **Estimated Time** | 15 Minutes |

---

## Background Theory

Netcat can transfer files by streaming raw bytes over an established TCP connection. Unlike protocols such as FTP or SFTP, Netcat does not implement authentication, encryption, compression, or integrity verification. Instead, it simply transmits data from the sender's standard input (`stdin`) to the receiver's standard output (`stdout`).

In this exercise:

- **Kali Linux** acts as the **Sender**.
- **Windows 11** acts as the **Receiver**.
- File integrity is verified using **SHA-256** after the transfer.

---

## File Transfer Workflow

```text
sample.txt
     │
     ▼
Standard Input (stdin)
     │
     ▼
Netcat (Sender)
     │
 TCP Stream
     │
     ▼
Netcat (Receiver)
     │
     ▼
Standard Output (stdout)
     │
     ▼
sample_received.txt
```

---

## Network Communication Flow

```mermaid
flowchart LR

subgraph HostOnly["VirtualBox Host-Only Network"]

Kali["💻 Kali Linux<br/>Sender"]

Windows["🖥️ Windows 11<br/>Receiver"]

File["📄 sample.txt"]

Received["📄 sample_received.txt"]

File --> Kali

Kali -- "TCP Port 5555" --> Windows

Windows --> Received

end
```

---

# Exercise 2.1 – Create the Sample File

Create a dedicated working directory and generate the file that will be transferred.

## Commands

```bash
mkdir -p ~/netcat-lab

cd ~/netcat-lab

cat > sample.txt << EOF
Netcat File Transfer Lab
Author: ShadowCipher

This file demonstrates TCP file transfer using Netcat.

EOF
```

### Verify the File

```bash
cat sample.txt
```

### Expected Output

```text
Netcat File Transfer Lab
Author: ShadowCipher

This file demonstrates TCP file transfer using Netcat.
```

### Evidence

**Figure 2.1 – Sample file created on Kali Linux**

> `screenshots/phase-2/01-create-sample-file.png`

---

# Exercise 2.2 – Configure the Receiver

On Windows 11, navigate to the working directory and start Netcat in listening mode.

## Commands

```powershell
cd ForLab

ncat -l 5555 > sample_received.txt
```

### Command Breakdown

| Command | Description |
|---------|-------------|
| `cd ForLab` | Navigate to the working directory |
| `ncat -l 5555` | Start Netcat in listening mode |
| `>` | Redirect received data into a file |

The listener will wait silently until the sender connects.

### Evidence

**Figure 2.2 – Windows waiting to receive the file**

> `screenshots/phase-2/02-listener.png`

---

# Exercise 2.3 – Transfer the File

From Kali Linux, send the contents of `sample.txt` to the Windows listener.

## Command

```bash
nc 192.168.56.102 5555 < sample.txt
```

### Command Breakdown

| Parameter | Description |
|-----------|-------------|
| `nc` | Launch Netcat |
| `192.168.56.102` | Windows 11 IP Address |
| `5555` | Destination TCP Port |
| `< sample.txt` | Redirect file contents into the TCP connection |

After the transfer completes, Netcat automatically closes the connection.

### Evidence

**Figure 2.3 – File successfully transmitted**

> `screenshots/phase-2/03-file-transfer.png`

---

# Exercise 2.4 – Verify the Received File

Display the received file on Windows.

## Command

```powershell
type sample_received.txt
```

### Expected Output

```text
Netcat File Transfer Lab
Author: ShadowCipher

This file demonstrates TCP file transfer using Netcat.
```

### Evidence

**Figure 2.4 – File successfully received**

> `screenshots/phase-2/04-received-file.png`

---

# Exercise 2.5 – Verify File Integrity

To ensure that the transferred file was not modified during transmission, compare the SHA-256 hash values on both systems.

## Kali Linux

```bash
sha256sum sample.txt
```

## Windows 11

```powershell
certutil -hashfile sample_received.txt SHA256
```

### Verification

The SHA-256 hashes generated on both systems should be identical.

Matching hash values confirm:

- The transfer completed successfully.
- No data corruption occurred.
- File integrity was preserved throughout transmission.

### Evidence

**Figure 2.5 – SHA-256 hash verification**

> `screenshots/phase-2/05-sha256-verification.png`

---

## Technical Analysis

During this exercise, Netcat established a reliable TCP connection between Kali Linux and Windows 11.

Instead of transmitting keyboard input, the contents of `sample.txt` were redirected from the sender's standard input (`stdin`) into the TCP socket. On the receiving side, Netcat redirected the incoming byte stream from its standard output (`stdout`) into `sample_received.txt`.

This demonstrates that Netcat transfers data as a continuous stream of bytes without interpreting file formats or metadata. As a result, the same technique can be used to transfer text files, configuration files, scripts, logs, or binary data.

To verify that the transfer completed successfully without corruption, SHA-256 hashes were generated on both systems. Matching hash values confirmed that the received file was identical to the original.

---

## Security Perspective

While Netcat is effective for demonstrating raw TCP file transfers, it does **not** provide:

- Authentication
- Encryption
- Integrity protection during transmission
- Access control

In enterprise environments, secure alternatives such as **SCP**, **SFTP**, **HTTPS**, or **SMB with encryption** should be used when transferring sensitive information.

Understanding how Netcat performs raw file transfers helps SOC analysts recognize legitimate administrative activity as well as identify suspicious data transfers during incident investigations.

---

## Real-World Applications

This technique can be used for:

- Network troubleshooting
- Testing TCP connectivity
- Transferring log files in isolated environments
- Demonstrating stream-based communication
- Validating firewall configurations
- Understanding data flow over TCP

---

## Troubleshooting

| Issue | Possible Cause | Resolution |
|--------|----------------|------------|
| Connection refused | Listener not started | Start the Windows listener before sending the file. |
| Empty output file | Sender command interrupted | Repeat the transfer. |
| Hash mismatch | File modified or incomplete transfer | Re-transfer the file and verify both hashes again. |
| Incorrect destination | Wrong IP address or port | Confirm the receiver's IP address and listening port. |

---

## Key Takeaways

- Successfully transferred a file using a raw TCP connection.
- Understood how shell redirection (`<` and `>`) works with Netcat.
- Learned how Netcat streams raw bytes without interpreting file contents.
- Verified successful transmission using SHA-256 hash comparison.
- Reinforced the reliability of TCP for file transfer.
- Gained practical experience with one of Netcat's most common networking use cases.

---
# Phase 3 – Zero-I/O Port Scanning Using Netcat

> **Objective:** Discover open TCP ports on multiple systems using Netcat's Zero-I/O mode to identify available network services without establishing an interactive session.

---

## Quick Summary

| Category | Details |
|----------|---------|
| **Objective** | Discover open TCP ports using Netcat |
| **Technique** | Zero-I/O TCP Port Scanning |
| **Protocol** | TCP |
| **Mode** | Zero-I/O (`-z`) |
| **Verbosity** | Enabled (`-v`) |
| **Tool** | Netcat (nc) |
| **Difficulty** | Beginner |
| **Estimated Time** | 15–20 Minutes |

---

## Background Theory

Port scanning is the process of identifying open network ports on a remote system. Each open port generally represents a service waiting for client connections, such as SSH, FTP, HTTP, or SMB.

Netcat provides a lightweight method of checking whether a TCP port is open using **Zero-I/O Mode**.

Unlike interactive connections, Zero-I/O mode attempts to establish a TCP connection without transmitting application data. This allows administrators and security analysts to quickly verify service availability while generating minimal network traffic.

This exercise demonstrates service discovery across three different systems within the laboratory environment:

- **Metasploitable2**
- **Windows 11**
- **OWASP Juice Shop**

---

## Network Communication Flow

```mermaid
flowchart LR

Scanner["💻 Kali Linux"]

Metasploitable["🖥️ Metasploitable2"]

Windows["🖥️ Windows 11"]

JuiceShop["🖥️ OWASP Juice Shop"]

Scanner -- "TCP Scan" --> Metasploitable

Scanner -- "TCP Scan" --> Windows

Scanner -- "TCP Scan" --> JuiceShop
```

---

## Understanding Netcat Scan Options

| Option | Description |
|---------|-------------|
| `-z` | Enables Zero-I/O mode (no data is transmitted). |
| `-v` | Displays verbose output, including connection status. |

---

# Exercise 3.1 – Scan Metasploitable2

Scan a range of TCP ports to identify running services.

## Command

```bash
nc -zv 192.168.56.101 20-1000
```

### Purpose

This command scans TCP ports **20 through 1000** on the Metasploitable2 virtual machine.

### Open Ports Discovered

| Port | Service |
|------|----------|
| 21 | FTP |
| 22 | SSH |
| 23 | Telnet |
| 25 | SMTP |
| 53 | DNS |
| 80 | HTTP |
| 111 | RPCBind |
| 139 | NetBIOS |
| 445 | SMB |
| 512 | rexec |
| 513 | rlogin |
| 514 | rsh |

### Evidence

**Figure 3.1 – TCP port scan of Metasploitable2**

> `screenshots/phase-3/01-metasploitable-range-scan.png`

---

# Exercise 3.2 – Verify MySQL Service

Instead of scanning a range, verify whether a specific service is available.

## Command

```bash
nc -zv 192.168.56.101 3306
```

### Purpose

Checks whether the MySQL database service is accepting TCP connections.

### Expected Result

```text
(UNKNOWN) [192.168.56.101] 3306 (mysql) open
```

### Evidence

**Figure 3.2 – MySQL service verification**

> `screenshots/phase-3/02-mysql-port.png`

---

# Exercise 3.3 – Scan Windows 11 Services

Scan common Windows networking ports.

## Command

```bash
nc -zv 192.168.56.107 135-139
```

### Open Ports Discovered

| Port | Service |
|------|----------|
| 135 | Microsoft RPC Endpoint Mapper |
| 139 | NetBIOS Session Service |

These services are commonly used by Windows for remote administration and file sharing.

### Evidence

**Figure 3.3 – Windows service scan**

> `screenshots/phase-3/03-windows-range-scan.png`

---

# Exercise 3.4 – Verify SMB Service

Check whether the SMB service is available.

## Command

```bash
nc -zv 192.168.56.107 445
```

### Expected Result

```text
(UNKNOWN) [192.168.56.107] 445 (microsoft-ds) open
```

### Purpose

Port **445** hosts the Server Message Block (SMB) protocol, which is widely used for:

- File sharing
- Printer sharing
- Windows authentication
- Active Directory communication

### Evidence

**Figure 3.4 – SMB service verification**

> `screenshots/phase-3/04-smb-port.png`

---

# Exercise 3.5 – Verify OWASP Juice Shop

Check whether the Juice Shop web application is accepting TCP connections.

## Command

```bash
nc -zv 192.168.56.105 3000
```

### Expected Result

```text
(UNKNOWN) [192.168.56.105] 3000 open
```

### Purpose

Port **3000** hosts the OWASP Juice Shop web application.

The successful connection confirms that the HTTP service is running and ready for subsequent testing.

### Evidence

**Figure 3.5 – OWASP Juice Shop service verification**

> `screenshots/phase-3/05-juice-shop-port.png`

---

## Verification Checklist

The exercise was considered successful when:

- ✅ Open TCP ports were successfully identified.
- ✅ Multiple hosts were scanned.
- ✅ Individual services were verified.
- ✅ Netcat correctly reported open ports.
- ✅ Service availability was confirmed without exchanging application data.

---

## Technical Analysis

Netcat's **Zero-I/O Mode** (`-z`) attempts to establish a TCP connection without transmitting application data.

For each target port, Netcat sends a TCP connection request. If the remote service responds positively, the port is reported as **open**. If no service is listening or the connection is refused, Netcat reports the port as closed or unreachable.

This lightweight scanning technique is useful for quickly confirming whether network services are available while generating minimal traffic.

---

## Security Perspective

Port scanning is one of the first techniques used during both network administration and security assessments.

For SOC analysts and defenders, port scanning helps to:

- Verify exposed services
- Detect unauthorized network services
- Validate firewall configurations
- Confirm system hardening
- Troubleshoot application connectivity
- Inventory enterprise assets

Understanding which services are exposed is essential for reducing an organization's attack surface and identifying unnecessary or vulnerable services.

---

## Real-World Applications

Zero-I/O scanning is commonly used for:

- Service availability verification
- Firewall validation
- Asset inventory
- Network troubleshooting
- Security assessments
- Baseline configuration verification

---

## Troubleshooting

| Issue | Possible Cause | Resolution |
|--------|----------------|------------|
| Connection refused | Service is not running | Verify the target service is active. |
| Host unreachable | Network connectivity issue | Confirm both systems are on the same network. |
| Timeout | Firewall blocking traffic | Review firewall rules and network ACLs. |
| Incorrect results | Wrong IP address or port range | Verify the target address and scan parameters. |

---

## Key Takeaways

- Learned how Netcat performs TCP Zero-I/O port scanning.
- Identified open network services across multiple hosts.
- Verified individual services without initiating interactive sessions.
- Improved understanding of common TCP ports and enterprise services.
- Reinforced the importance of service discovery in network security and troubleshooting.
- Gained practical experience with one of Netcat's most useful administrative capabilities.

---
# Phase 4 – Banner Grabbing & Service Enumeration

> **Objective:** Identify running network services by connecting to open TCP ports and analyzing the service banners returned by the target systems.

---

## Quick Summary

| Category | Details |
|----------|---------|
| **Objective** | Identify network services through banner grabbing |
| **Technique** | Service Enumeration |
| **Protocol** | TCP |
| **Tool** | Netcat (nc) |
| **Target** | Metasploitable2 |
| **Difficulty** | Beginner |
| **Estimated Time** | 15 Minutes |

---

## Background Theory

Banner grabbing is the process of connecting to a network service and reading the information it provides immediately after a successful connection. Many services transmit a banner containing useful information such as:

- Service name
- Software version
- Protocol version
- Operating system information
- Vendor details

This information helps administrators verify service configurations and assists security professionals in identifying systems and validating network inventories.

Unlike vulnerability scanning, banner grabbing is a passive service identification technique that simply observes information voluntarily presented by the remote service.

---

## Service Enumeration Workflow

```mermaid
flowchart LR

Scanner["💻 Kali Linux"]

Target["🖥️ Metasploitable2"]

Banner["Service Banner"]

Scanner -->|"TCP Connection"| Target

Target -->|"FTP / SSH / SMTP Banner"| Banner

Banner --> Scanner
```

---

# Exercise 4.1 – Enumerate FTP Service

Connect to the FTP service running on Metasploitable2.

## Command

```bash
nc 192.168.56.101 21
```

### Expected Output

```text
220 (vsFTPd 2.3.4)
```

### Technical Explanation

The FTP server immediately returns its service banner after the TCP connection is established.

The banner identifies:

- Service: FTP
- Software: vsFTPd
- Version: 2.3.4

### Evidence

**Figure 4.1 – FTP banner returned by the server**

> `screenshots/phase-4/01-ftp-banner.png`

---

# Exercise 4.2 – Enumerate SSH Service

Connect to the SSH service.

## Command

```bash
nc 192.168.56.101 22
```

### Expected Output

```text
SSH-2.0-OpenSSH_4.7p1 Debian-8ubuntu1
```

### Technical Explanation

Unlike FTP, SSH immediately advertises its protocol version before authentication begins.

The banner provides:

- Protocol Version: SSH-2.0
- Software: OpenSSH
- Version: 4.7p1
- Platform: Debian

Your terminal may also display:

```text
Protocol mismatch.
```

This occurs because Netcat is not an SSH client. After reading the banner, it sends unexpected input, causing the SSH server to terminate the session. This behavior is expected and confirms that the SSH service is functioning correctly.

### Evidence

**Figure 4.2 – SSH banner returned by the server**

> `screenshots/phase-4/02-ssh-banner.png`

---

# Exercise 4.3 – Enumerate SMTP Service

Connect to the SMTP service.

## Command

```bash
nc 192.168.56.101 25
```

### Expected Output

```text
220 metasploitable.localdomain ESMTP Postfix (Ubuntu)
```

### Technical Explanation

SMTP servers transmit a greeting banner immediately after a client connects.

The returned banner identifies:

- Service: SMTP
- Mail Server: Postfix
- Operating System: Ubuntu

### Evidence

**Figure 4.3 – SMTP banner returned by the server**

> `screenshots/phase-4/03-smtp-banner.png`

---

## Verification Checklist

The exercise was considered successful when:

- ✅ FTP banner was successfully retrieved.
- ✅ SSH banner identified the protocol and software version.
- ✅ SMTP banner identified the mail server.
- ✅ Service versions matched the expected applications.
- ✅ All banners were obtained using simple TCP connections.

---

## Technical Analysis

Banner grabbing relies on the behavior of application-layer protocols that voluntarily send identifying information immediately after a TCP connection is established.

Netcat acts as a lightweight TCP client, allowing direct interaction with these services without requiring protocol-specific software.

The retrieved banners provide valuable operational information, including service type, software implementation, protocol version, and in some cases, operating system details. This information is useful for validating system configurations, confirming service availability, and understanding the software stack running on a host.

---

## Security Perspective

Banner grabbing is widely used during:

- Asset inventory
- Network troubleshooting
- Security assessments
- Vulnerability management
- Incident response
- Configuration validation

From a defensive standpoint, unnecessary banner disclosure can reveal software versions that may assist attackers in identifying outdated or vulnerable services. For this reason, many organizations configure production systems to minimize or suppress service banners where possible.

---

## Real-World Applications

Banner grabbing helps administrators and security professionals:

- Identify active network services.
- Verify software versions.
- Confirm protocol implementations.
- Troubleshoot service availability.
- Validate configuration changes.
- Maintain accurate asset inventories.

---

## Troubleshooting

| Issue | Possible Cause | Resolution |
|--------|----------------|------------|
| Connection refused | Service is not running | Verify the target service is active. |
| No banner returned | Service does not disclose banners | Confirm using protocol-specific clients if necessary. |
| Protocol mismatch | Netcat is not a protocol-aware client | Expected behavior when connecting to services such as SSH. |
| Timeout | Firewall or connectivity issue | Verify network connectivity and firewall configuration. |

---

## Key Takeaways

- Learned how to identify network services using banner grabbing.
- Enumerated FTP, SSH, and SMTP services.
- Interpreted service banners to identify software and protocol versions.
- Understood why some services immediately transmit identifying information.
- Recognized the security implications of banner disclosure.
- Strengthened practical service enumeration skills applicable to network administration and security operations.

---
# Phase 5 – HTTP Request Testing Using Netcat

> **Objective:** Manually construct and transmit an HTTP request over a raw TCP connection using Netcat to understand the structure of the HTTP protocol and analyze the server's response.

---

## Quick Summary

| Category | Details |
|----------|---------|
| **Objective** | Test an HTTP service using a manually crafted HTTP request |
| **Protocol** | HTTP over TCP |
| **Target Service** | OWASP Juice Shop |
| **Target Port** | 3000 |
| **Tool** | Netcat (nc) |
| **Difficulty** | Intermediate |
| **Estimated Time** | 15–20 Minutes |

---

## Background Theory

Hypertext Transfer Protocol (HTTP) is an application-layer protocol that operates over TCP. Before a web browser renders a webpage, it sends a properly formatted HTTP request to the web server.

An HTTP/1.1 request consists of:

- A request line
- One or more headers
- A blank line indicating the end of the headers

If required headers are missing or the request format is invalid, the server returns an HTTP error response such as **400 Bad Request**.

This exercise demonstrates how to manually build and transmit an HTTP request using Netcat without relying on a browser or specialized HTTP client.

---

## HTTP Communication Flow

```mermaid
sequenceDiagram

participant Kali as 💻 Kali Linux
participant Juice as 🧃 OWASP Juice Shop

Kali->>Juice: TCP Connection (Port 3000)

Kali->>Juice: HTTP GET Request

Juice-->>Kali: HTTP/1.1 200 OK

Juice-->>Kali: HTML Document
```

---

# Exercise 5.1 – Initial HTTP Request

Connect to the OWASP Juice Shop application.

## Command

```bash
nc 192.168.56.105 3000
```

After the TCP connection is established, attempt to send the HTTP request manually.

```http
GET / HTTP/1.1
```

### Actual Result

```text
HTTP/1.1 400 Bad Request
Connection: close
```

### Why Did This Happen?

HTTP/1.1 requires the **Host** header to identify the destination virtual host.

Because only the request line was transmitted, the web server detected an incomplete request and responded with:

```text
400 Bad Request
```

This behavior is expected and confirms that the server is correctly validating the HTTP request format.

### Evidence

**Figure 5.1 – Initial HTTP request resulting in a 400 Bad Request**

> `screenshots/phase-5/01-http-400.png`

---

# Exercise 5.2 – Construct a Valid HTTP Request

Instead of typing the request interactively, generate a complete HTTP request using `printf` and pipe it into Netcat.

## Command

```bash
printf "GET / HTTP/1.1\r\nHost: 192.168.56.105\r\nConnection: close\r\n\r\n" | nc 192.168.56.105 3000
```

### Command Breakdown

| Component | Description |
|-----------|-------------|
| `printf` | Constructs the HTTP request |
| `GET / HTTP/1.1` | Requests the root resource |
| `Host:` | Required header for HTTP/1.1 |
| `Connection: close` | Requests the server to close the connection after sending the response |
| `\r\n` | Carriage Return + Line Feed (HTTP line terminator) |
| `|` | Pipes the generated request into Netcat |
| `nc` | Sends the request through the TCP connection |

---

## Expected Response

```http
HTTP/1.1 200 OK
```

Followed by:

- HTTP headers
- HTML document
- JavaScript references
- CSS references

The response confirms that the web server successfully processed the request.

### Evidence

**Figure 5.2 – Successful HTTP response (200 OK) from OWASP Juice Shop**

> `screenshots/phase-5/02-http-200.png`

---

## Verification Checklist

The exercise was considered successful when:

- ✅ A TCP connection to the web server was established.
- ✅ An initial malformed request produced **400 Bad Request**.
- ✅ A correctly formatted HTTP request returned **200 OK**.
- ✅ HTTP headers were successfully displayed.
- ✅ The HTML source code of the application was received.

---

## Technical Analysis

Initially, the request contained only the HTTP request line and omitted the mandatory `Host` header required by HTTP/1.1. As a result, the server could not determine the requested virtual host and returned a **400 Bad Request** response.

The corrected request included all required components:

- Request line
- Host header
- Connection header
- Blank line terminating the header section

Using `printf` ensured that the request was formatted with the required **CRLF (`\r\n`)** line endings defined by the HTTP specification. Once the server received a valid request, it responded with **HTTP/1.1 200 OK**, followed by the complete HTML document for the OWASP Juice Shop application.

---

## Security Perspective

Understanding raw HTTP communication is an essential skill for cybersecurity professionals.

SOC analysts, penetration testers, and web security engineers frequently inspect raw HTTP requests and responses when:

- Investigating web application attacks
- Analyzing proxy logs
- Troubleshooting API communication
- Validating HTTP headers
- Identifying malformed requests
- Reviewing packet captures

Being able to manually construct HTTP requests helps analysts understand how web applications communicate at the protocol level.

---

## Real-World Applications

This technique is useful for:

- Testing web servers without a browser
- Understanding HTTP protocol structure
- Troubleshooting application connectivity
- Learning how browsers communicate with servers
- Verifying HTTP responses
- Debugging web applications

---

## Troubleshooting

| Issue | Possible Cause | Resolution |
|--------|----------------|------------|
| HTTP 400 Bad Request | Missing required HTTP headers | Include the `Host` header and terminate headers with a blank line. |
| No response | Incorrect IP address or port | Verify the target address and ensure the web application is running. |
| Connection refused | Service not running | Start the OWASP Juice Shop application before testing. |
| Incomplete response | Incorrect line endings | Use `\r\n` when constructing the HTTP request. |

---

## Key Takeaways

- Established a TCP connection to a web server using Netcat.
- Learned the structure of an HTTP/1.1 request.
- Understood why the `Host` header is mandatory in HTTP/1.1.
- Successfully transmitted a manually crafted HTTP request.
- Received and analyzed an **HTTP/1.1 200 OK** response.
- Reinforced the relationship between TCP and HTTP in client-server communication.

---
---

# Project Summary

This project explored the practical use of **Netcat (nc)** as a lightweight networking utility for communication, testing, service validation, and troubleshooting within a controlled virtual laboratory environment.

Rather than relying on automated security scanners or graphical applications, each exercise focused on interacting directly with network services through the command line. This approach provided a deeper understanding of how TCP-based communication operates at the protocol level and how many common administrative and security tasks can be performed using a single utility.

The laboratory consisted of five structured exercises, progressing from basic TCP communication to service discovery and manual HTTP interaction. Every phase was performed in a VirtualBox-based lab using Kali Linux, Windows 11, Metasploitable2, and OWASP Juice Shop, with all commands, outputs, observations, and screenshots documented throughout this repository.

---

# Technical Skills Demonstrated

Throughout this project, the following practical networking and cybersecurity skills were developed and demonstrated:

### Networking Fundamentals

- TCP client-server communication
- TCP socket establishment and termination
- Understanding listeners and client connections
- Network connectivity verification
- Host-Only virtual networking

### Netcat Operations

- Creating TCP listeners
- Initiating client connections
- File transfer over raw TCP streams
- Zero-I/O TCP port scanning
- Service validation
- Banner grabbing
- Manual HTTP request generation
- Network troubleshooting

### Protocol Analysis

- TCP communication workflow
- File transmission over TCP
- HTTP request formatting
- HTTP response analysis
- Service identification through banners
- Common network ports and services

### Operating Systems

- Kali Linux
- Windows 11
- Linux Command Line
- Windows PowerShell

### Documentation

- Technical documentation
- Markdown authoring
- Professional GitHub project organization
- Screenshot-based laboratory reporting

---

# Key Learning Outcomes

Completing this laboratory significantly strengthened my understanding of network communication and protocol behavior.

Some of the most valuable learning outcomes include:

- Understanding how TCP establishes reliable client-server communication.
- Learning how Netcat functions as both a client and a listener.
- Transferring files over raw TCP streams and validating integrity using SHA-256 hashing.
- Discovering active network services through Zero-I/O port scanning.
- Identifying applications by analyzing service banners.
- Understanding the structure of HTTP requests and responses.
- Learning why HTTP/1.1 requires mandatory headers such as the `Host` header.
- Troubleshooting connectivity and protocol-related issues within a virtual networking environment.
- Developing confidence working directly with networking tools instead of relying solely on graphical interfaces.

Most importantly, this project reinforced the value of understanding networking fundamentals before moving on to advanced security tools such as Nmap, Wireshark, SIEM platforms, vulnerability scanners, and intrusion detection systems.

---

# Challenges Encountered and Solutions

Like any practical laboratory, this project involved several technical challenges that required investigation and troubleshooting.

| Challenge | Resolution |
|-----------|------------|
| Windows initially did not recognize the `ncat` command | Installed the official Nmap package, which includes Ncat. |
| ICMP ping requests from Kali to Windows failed | Verified that TCP communication worked correctly and confirmed Host-Only network connectivity. |
| Initial HTTP request returned **400 Bad Request** | Identified the missing `Host` header and corrected the request using `printf` with proper CRLF formatting. |
| Understanding why SSH returned `Protocol mismatch` | Learned that Netcat is not an SSH client and that the SSH server was correctly rejecting unexpected input after transmitting its banner. |
| Verifying file integrity after transfer | Compared SHA-256 hashes on both systems to confirm successful transmission without data corruption. |

These challenges provided valuable troubleshooting experience that closely resembles the investigative process required in real-world IT and cybersecurity environments.

---

# Practical Applications

Although Netcat is a lightweight utility, the concepts demonstrated throughout this project directly relate to everyday operational tasks performed by network engineers, system administrators, and security analysts.

Some practical applications include:

- Network troubleshooting
- Service availability verification
- Connectivity testing
- File transfer in isolated environments
- Network diagnostics
- Firewall validation
- Service enumeration
- Basic protocol analysis
- Security assessments
- Incident response investigations

Understanding these foundational techniques provides valuable context for working with enterprise networking and security technologies.

---

# Future Enhancements

This repository serves as a foundation for learning networking with Netcat. Future improvements may include:

- UDP communication using Netcat
- IPv6 networking exercises
- Secure communication using Ncat's SSL/TLS capabilities
- Packet capture and protocol analysis with Wireshark
- Python socket programming examples
- Bash scripting to automate common networking tasks
- Firewall testing and rule validation
- Additional HTTP methods (POST, PUT, DELETE)
- Simple client-server applications
- Integration with SIEM and network monitoring platforms

These additions will expand the project while continuing to emphasize practical networking knowledge.

---

# References

The following resources were used for research and technical verification throughout this project:

- Netcat (`nc`) Manual Pages
- Ncat User Guide (Nmap Project)
- RFC 793 – Transmission Control Protocol (TCP)
- RFC 9112 – HTTP/1.1
- OWASP Juice Shop Documentation
- Oracle VirtualBox Documentation
- Kali Linux Documentation

---

# Conclusion

This project demonstrates the practical application of Netcat within a controlled virtual networking laboratory while reinforcing the networking concepts that underpin modern information technology and cybersecurity.

Across five structured phases, I successfully established TCP client-server communication, transferred files across the network, performed Zero-I/O port scanning, identified network services through banner grabbing, and manually constructed HTTP requests to interact directly with a web application.

Beyond learning individual Netcat commands, this project emphasized understanding **why** each command works, **how** TCP-based communication occurs, and **what** information can be obtained through direct interaction with network services.

Documenting each phase with commands, explanations, diagrams, screenshots, troubleshooting notes, and technical observations also strengthened my ability to produce clear and reproducible technical documentation—an essential skill for cybersecurity professionals.

Overall, this repository represents not only a collection of Netcat exercises but also a practical demonstration of foundational networking knowledge, analytical thinking, troubleshooting methodology, and technical communication. These are core competencies that support roles in **Network Security**, **Security Operations Centers (SOC)**, **System Administration**, and **IT Infrastructure**.

---

# Acknowledgements

This project was completed as part of my personal cybersecurity learning journey to strengthen practical networking knowledge through hands-on laboratory exercises.

I would like to acknowledge the open-source communities and projects whose software made this laboratory possible:

- Nmap / Ncat
- Kali Linux
- Oracle VirtualBox
- Metasploitable2
- OWASP Juice Shop

Their contributions continue to provide valuable learning resources for students, researchers, and cybersecurity professionals worldwide.

---
