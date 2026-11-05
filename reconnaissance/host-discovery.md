# Host Discovery

## 1. Overview

Host discovery is the initial reconnaissance stage of a network security assessment. It involves identifying whether a target machine is active and reachable within a network.

In this investigation, connectivity between the Ubuntu analyst machine and the Metasploitable 2 target was examined within an isolated VirtualBox host-only network.

The investigation involved identifying the target IP address, testing connectivity using ICMP and performing host discovery using Nmap.

## 2. Objectives

- Identify the IP address of the target machine.
- Verify connectivity between the analyst machine and the target.
- Determine whether the target responds to ICMP Echo Requests.
- Perform host discovery using Nmap.
- Confirm that the lab environment is ready for further network reconnaissance.

## 3. Lab Environment

| Component | Details |
|---|---|
| Network Range | 192.168.56.0/24 |
| Analyst IP | 192.168.56.101 |
| Target IP | 192.168.56.102 |

## 4. Methodology

### 4.1 Identifying the Target IP Address

Before conducting network reconnaissance, the IP address of the Metasploitable 2 target had to be identified.

Both virtual machines were configured to communicate through a VirtualBox Host-only Network. This created an isolated network that allowed the analyst machine and target to communicate.

The network interface configuration was checked within Metasploitable 2 using:


ifconfig

The command displayed the available network interfaces and their assigned IP addresses. The interface connected to the host-only network was identified, and its assigned IP address was: 

* **Target IP:** `192.168.56.102`
* **Analyst IP:** `192.168.56.101` (The Ubuntu analyst machine on the same network)

Both addresses belonged to the `192.168.56.0/24` subnet, allowing communication between the two virtual machines.

### 4.2 Testing Connectivity Using Ping
The first connectivity test was performed using Ping to determine whether the target responded to ICMP Echo Requests.

* **Command:** `ping -c 4 192.168.56.102`
* **Command explanation:**
  * `ping` — Sends ICMP Echo Requests to a target and listens for replies.
  * `-c 4` — Limits the test to four packets.
  * `192.168.56.102` — IP address of the Metasploitable 2 target.

#### Observed Results

| Metric | Result |
| :--- | :--- |
| Packets transmitted | 4 |
| Packets received | 4 |
| Packet loss | 0% |

#### Observations
* All four ICMP Echo Requests received replies from the target.
* No packet loss was recorded.
* The target was reachable from the Ubuntu analyst machine.
* The responses also displayed a TTL value of 64. 

> **Note:** TTL (Time To Live) limits the number of network hops an IP packet can travel before being discarded.

---

### 4.3 Host Discovery Using Nmap
After confirming connectivity using Ping, Nmap was used to determine whether the target was active on the network.

* **Command:** `nmap -sn 192.168.56.102`
* **Command explanation:**
  * `nmap` — Network exploration and security auditing tool.
  * `-sn` — Performs host discovery without conducting a port scan.
  * `192.168.56.102` — Specifies the target IP address.

#### Observed Results
```text
Starting Nmap 7.98 Nmap scan report for 192.168.56.102
Host is up (0.018s latency).
Nmap done: 1 IP address (1 host up) scanned in 4.54 seconds
```

#### Observations
* Nmap identified the target as active.
* The reported latency was approximately 18 milliseconds.
* One IP address was scanned, and one active host was identified.
* The result confirmed the connectivity observations obtained through Ping.

---

### 5. Results and Analysis
Both Ping and Nmap successfully identified the Metasploitable 2 machine as reachable.

#### Test Result Interpretation

| IP Identification | 192.168.56.102 Target address identified |
| :--- | :--- |
| **ICMP Ping** | 4 replies received; Target responded to connectivity requests |
| **Packet Loss** | 0% packet loss during the test |
| **Nmap Host Discovery** | Host is up; Target identified as active |
| **Nmap Latency** | 0.018 seconds; Target responded within approximately 18 ms |

The two tools provided complementary information:
* **Ping** verified basic network connectivity through ICMP Echo Requests and Replies.
* **Nmap** independently identified the target as an active host.

This confirmed that communication between the analyst machine and the target was working, allowing the assessment to proceed to port scanning and service enumeration.

---

### 6. Evidence
The following evidence supports the host discovery investigation:

* **Evidence Description:** Host Discovery Screenshot
* **Terminal Output:** Showing successful Ping and Nmap host discovery results.
* **The screenshot contains:**
  * `ping -c 4 192.168.56.102` and its output.
  * `nmap -sn 192.168.56.102` and its output.

> **Note:** The target IP identification step is documented as part of the methodology. No screenshot was retained for that step.

---

### 7. Conclusion
The host discovery stage successfully established that the Metasploitable 2 target was active and reachable from the Ubuntu analyst machine. 

The target IP address was identified from its network interface configuration. Ping returned four successful ICMP replies with no packet loss, while Nmap independently confirmed that the target was up. With connectivity established, the investigation could proceed to TCP and UDP port scanning to identify network services exposed by the target.

---

### 8. Skills Demonstrated
* Network configuration and IP addressing
* Host-only network configuration
* Network connectivity testing
* ICMP protocol
* Nmap host discovery
* Linux command-line operations
* Network reconnaissance
* Interpretation of network diagnostic results
