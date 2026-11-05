# Network Security Assessment

## Overview

A hands-on network security assessment conducted in an isolated VirtualBox environment to investigate network connectivity, identify exposed services, capture network traffic and analyse communication protocols.

The project focuses on practical network reconnaissance, service enumeration, traffic analysis and security investigation using networking and packet analysis tools.

The assessment uses an Ubuntu virtual machine as the analyst machine and Metasploitable 2 as the target system.

## Objectives

- Identify active hosts within an isolated network.
- Perform network reconnaissance and host discovery.
- Identify open TCP and UDP ports.
- Enumerate running services and their versions.
- Investigate network communication using packet captures.
- Analyse ICMP, TCP, HTTP and DNS traffic.
- Compare plaintext communication using Telnet with encrypted communication using SSH.
- Identify potential network security weaknesses.
- Document findings and supporting evidence.
- Develop appropriate security recommendations.

## Environment

- **Analyst Operating System:** Ubuntu Linux
- **Target Operating System:** Metasploitable 2
- **Virtualization:** Oracle VirtualBox 7.2.14
- **Network Configuration:** Host-only network
- **Lab Network:** 192.168.56.0/24
- **Analyst IP:** 192.168.56.101
- **Target IP:** 192.168.56.102
- **Shell:** Bash

## Tools & Technologies

| Tool             | Purpose                                                |
|------------------|--------------------------------------------------------|
| Nmap             | Host discovery, port scanning and service enumeration |
| Tcpdump          | Network traffic capture                               |
| Wireshark        | Packet inspection and protocol analysis               |
| Curl             | HTTP request and response investigation               |
| Nslookup         | DNS queries and response analysis                     |
| Telnet           | Plaintext remote communication analysis               |
| SSH              | Encrypted remote communication analysis               |
| Ubuntu Linux     | Analyst environment                                    |
| Metasploitable 2 | Intentionally vulnerable target                       |

## Network Security Areas

| #  | Security Area                       | Status      |
|----|-------------------------------------|-------------|
| 1  | Host Discovery                      | Completed   |
| 2  | TCP Port Scanning                   | Completed   |
| 3  | Service Enumeration                 | Completed   |
| 4  | ICMP Traffic Analysis               | Completed   |
| 5  | TCP Traffic Analysis                | Completed   |
| 6  | HTTP Traffic Analysis               | Completed   |
| 7  | DNS Analysis                        | Completed   |
| 8  | Telnet vs SSH Analysis              | Completed   |
| 9  | Security Findings & Recommendations | Completed|
| 10 | Final Assessment Report             | Completed     |

## Security Investigations

### 1. Host Discovery

**Status:** Completed

Investigated connectivity between the Ubuntu analyst machine and the Metasploitable 2 target.

The investigation included:

- Verifying network interface configuration.
- Identifying the route to the target.
- Testing connectivity using ICMP echo requests.
- Performing host discovery using Nmap.
- Examining the local neighbour table and MAC address information.

**Skills demonstrated:**

- Network connectivity testing
- IP addressing and subnetting
- ICMP
- ARP and neighbour discovery
- Network interface identification
- Nmap host discovery

**Detailed investigation:** [host-discovery.md](reconnaissance/host-discovery.md)

---

### 2. Port Scanning

**Status:** Completed

Performed TCP and UDP port scanning against the Metasploitable 2 target to identify exposed network services.

The investigation included:

- Identifying open TCP ports using Nmap.
- Investigating commonly exposed network services.
- Performing a targeted UDP scan against DNS port 53.
- Examining the potential attack surface created by exposed services.

**Skills demonstrated:**

- TCP and UDP
- Port scanning
- Nmap
- Network service identification
- Attack surface assessment

**Detailed investigation:** [port-scanning.md](reconnaissance/port-scanning.md)

---

### 3. Service Enumeration

**Status:** Completed

Investigated the services running on the target to identify their names, versions and basic characteristics.

The investigation included:

- Performing service and version detection using Nmap.
- Identifying service banners and version information.
- Investigating HTTP services using Curl.
- Examining HTTP response headers and server information.
- Investigating web application redirects.
- Checking the availability of the conventional HTTPS port (443).

**Skills demonstrated:**

- Service enumeration
- Nmap version detection
- Banner identification
- HTTP investigation
- HTTP response analysis
- Curl
- Service exposure assessment

**Detailed investigation:** [service-enumeration.md](reconnaissance/service-enumeration.md)

---

### 4. Network Traffic Analysis

**Status:** Completed

Captured and investigated network traffic to understand how devices communicate and how different protocols operate.

The investigation included:

- Capturing ICMP echo requests and replies.
- Observing ARP requests and responses.
- Examining TCP three-way handshakes.
- Analysing TCP sequence numbers, acknowledgements and flags.
- Investigating HTTP requests and responses.
- Examining DNS queries and responses.
- Comparing TCP-based Telnet and SSH communication.
- Identifying the difference between plaintext and encrypted traffic.

**Skills demonstrated:**

- Packet capture
- Tcpdump
- Wireshark
- ICMP analysis
- ARP analysis
- TCP protocol analysis
- HTTP analysis
- DNS analysis
- SSH and Telnet comparison
- Network protocol investigation

**Detailed investigations:**

- [ICMP Analysis](packet-analysis/icmp-analysis.md)
- [TCP Analysis](packet-analysis/tcp-analysis.md)
- [HTTP Analysis](packet-analysis/http-analysis.md)
- [DNS Analysis](packet-analysis/dns-analysis.md)
- [Telnet vs SSH](packet-analysis/telnet-vs-ssh.md)

---

## Security Findings

Potential security concerns identified during the assessment include:

- Plaintext communication through Telnet, which can expose session information.
- Unencrypted HTTP communication, allowing transmitted application data to be observed.
- Multiple exposed network services, increasing the target's attack surface.
- Legacy service versions requiring further investigation into support status and known security vulnerabilities.

These observations will be assessed and documented with supporting evidence and recommendations.

**Detailed findings:** [Findings Register](findings/findings-register.md)

## Skills Demonstrated

### Network Security

- Network reconnaissance
- Host discovery
- TCP and UDP port scanning
- Service enumeration
- Attack surface identification
- Network protocol analysis
- Plaintext and encrypted communication comparison

### Packet Analysis

- Network traffic capture
- Packet inspection
- TCP three-way handshake analysis
- TCP sequence and acknowledgement numbers
- ICMP and ARP investigation
- HTTP request and response analysis
- DNS query and response analysis
- Wireshark protocol dissection

### Technical Skills

- Linux command line
- Bash
- Nmap
- Tcpdump
- Wireshark
- Curl
- Nslookup
- VirtualBox
- Network troubleshooting
- Technical documentation

## Evidence

Supporting screenshots and approved packet captures are maintained in the `evidence/` directory.

Evidence will be organised according to the different stages of the assessment.

Packet captures containing sensitive information, including plaintext Telnet credentials, will not be published in the public repository.

## Methodology

The assessment follows a structured network security investigation process:

1. **Scope Definition** — Establish the target system and the boundaries of the assessment.
2. **Reconnaissance** — Identify reachable hosts and discover open ports.
3. **Enumeration** — Investigate exposed services and their versions.
4. **Traffic Capture** — Capture network communications using Tcpdump.
5. **Analysis** — Examine captured packets and identify protocol behaviour using Wireshark.
6. **Findings** — Identify potential security weaknesses and assess their implications.
7. **Documentation** — Record commands, observations, evidence and recommendations.

## Disclaimer

This project was conducted in an isolated VirtualBox lab using Metasploitable 2 for educational and portfolio purposes.

All testing was limited to the controlled lab environment. No unauthorised external or production systems were targeted.

## Project Structure

```text
network-security-assessment/
│
├── README.md
│
├── reconnaissance/
│   ├── host-discovery.md
│   ├── port-scanning.md
│   ├── service-enumeration.md
│   └── nmap-results/
│
├── packet-analysis/
│   ├── icmp-analysis.md
│   ├── tcp-analysis.md
│   ├── http-analysis.md
│   ├── dns-analysis.md
│   └── telnet-vs-ssh.md
│
├── evidence/
│   ├── screenshots/
│   └── packet-captures/
│
├── findings/
│   └── findings-register.md
│
└── reports/
    └── final-assessment-report.md

