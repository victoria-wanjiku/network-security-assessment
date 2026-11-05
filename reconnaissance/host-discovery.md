# Host Discovery

## Objective

The objective of this activity was to identify and verify the availability of a target machine within an isolated virtual network.

The exercise focused on:

- Identifying the target machine's IP address.
- Understanding the network configuration.
- Verifying connectivity between virtual machines.
- Using ICMP to test network reachability.
- Using Nmap for host discovery.
- Interpreting host discovery results.

---

## Environment

- **Network Type:** Host-only network
- **Network Subnet:** `192.168.56.0/24`
- **Analyst IP Address:** `192.168.56.101`
- **Target IP Address:** `192.168.56.102`
- **Network Interface:** `enp0s8` (Ubuntu host-only adapter)
- **Tools:** Ping, Nmap

Both virtual machines were connected through the VirtualBox host-only network, allowing them to communicate within an isolated lab environment.

---

## 1. Identifying the Target IP Address

Before performing host discovery, the target machine's IP address needed to be identified.

The Metasploitable 2 virtual machine was started, and its network configuration was checked using:

```bash
ifconfig
```

Alternatively, the following command can be used:

```bash
ip addr
```

These commands display network interfaces and their assigned IP addresses.

The IP address assigned to the target's host-only network interface was identified as:

```text
192.168.56.102
```

The Ubuntu analyst machine was also checked to confirm its host-only network address:

```bash
ip addr
```

Its host-only interface, `enp0s8`, had the address:

```text
192.168.56.101
```

Both machines were therefore within the same subnet:

```text
192.168.56.0/24
```

This confirmed that the two virtual machines were configured to communicate over the same host-only network.

---

## 2. Verifying Network Connectivity

Before scanning the target, connectivity was tested using the `ping` command.

The following command was executed from the Ubuntu analyst machine:

```bash
ping -c 4 192.168.56.102
```

**Command explanation:**

- `ping` sends ICMP Echo Request packets to test whether a target is reachable.
- `-c 4` limits the test to four packets.
- `192.168.56.102` is the target machine's IP address.

### Results

The target responded to all four ICMP Echo Requests.

The observed results were:

| Metric | Result |
|---|---|
| Packets transmitted | 4 |
| Packets received | 4 |
| Packet loss | 0% |
| Minimum round-trip time | 1.796 ms |
| Average round-trip time | 2.999 ms |
| Maximum round-trip time | 5.726 ms |
| TTL | 64 |

### Observations

- All four packets received responses from the target.
- No packet loss was observed during the test.
- The average round-trip time was approximately 3 ms.
- The TTL value of 64 represented the remaining IP packet lifetime reported in the replies.

The results confirmed that the Ubuntu machine could communicate with the Metasploitable 2 target over the host-only network.

### Evidence

![Ping connectivity test](../evidence/screenshots/ping-connectivity.png)

---

## 3. Performing Host Discovery with Nmap

After confirming connectivity, Nmap was used to perform host discovery.

The following command was executed:

```bash
nmap -sn 192.168.56.102
```

**Command explanation:**

- `nmap` is a network scanning tool used to discover hosts and identify services running on networked systems.
- `-sn` performs host discovery without conducting a port scan.
- `192.168.56.102` specifies the target IP address.

This scan was used to determine whether Nmap could identify the target as active on the network without enumerating its open ports.

### Results

Nmap reported the following:

```text
Nmap scan report for 192.168.56.102
Host is up (0.018s latency).
Nmap done: 1 IP address (1 host up) scanned in 4.54 seconds
```

### Observations

- **Host Status:** Nmap identified the target as up.
- **Latency:** Nmap reported a response time of approximately 18 milliseconds.
- **Discovery Result:** One IP address was scanned, and one active host was identified.

The latency value provided an indication of how quickly the target responded to Nmap's discovery probe during the test.

### Evidence

![Nmap host discovery](../evidence/screenshots/nmap-host-discovery.png)

---

## 4. Results and Observations

The host discovery activity successfully identified and verified the target machine within the isolated VirtualBox network.

The following table summarizes the results:

| Test | Result | Observation |
|---|---|---|
| Target IP identification | `192.168.56.102` | Target address identified from its network configuration |
| Network connectivity | Successful | Four ICMP Echo Replies received |
| Packet loss | 0% | No packet loss during the ping test |
| Nmap host discovery | Host up | Target identified as active |
| Nmap latency | 0.018 seconds | Target responded within approximately 18 ms |

The tests established that the target was reachable and available for subsequent network reconnaissance activities.

---

## Conclusion

Host discovery was successfully performed within the isolated VirtualBox environment.

The target machine's IP address was identified, connectivity was verified using ICMP, and Nmap confirmed that the target was active on the network.

This activity established the network connection required for the next stages of the assessment, including TCP port scanning and service enumeration.

All testing was conducted within a controlled virtual lab environment for educational and portfolio purposes.
