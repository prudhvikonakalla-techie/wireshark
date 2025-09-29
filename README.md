# Wireshark Network Traffic Analysis

## Objective
Capture and analyze network packets using Wireshark. Apply protocol-based filters to identify and inspect network traffic, including ARP, DNS, HTTP, and TCP protocols.

## Setup and Capture
- Installed Wireshark on Kali Linux.
- Started capture on interface `eth0` to collect live network traffic.
- Generated network activities such as web browsing, DNS queries, and HTTP logins.
- Stopped capture after sufficient data collection and saved the capture file (`.pcapng`).

## Protocol Filters and Analysis

### ARP Traffic
- **Filter:** `arp`
  !(/images/Screenshot 2025-09-29 194505.png)
- **Description:**  
  Displays Address Resolution Protocol packets used for IP-to-MAC address resolution on the local network.  
  Includes ARP requests (broadcast to find MAC for an IP) and ARP replies (direct responses with MAC addresses).  
  Useful for network troubleshooting and detecting ARP spoofing attacks.

### DNS Traffic
- **Filters:**
- 
  - `ip.src == <host_ip>` (e.g., `ip.src == 10.199.92.19`) to view all traffic originating from the host.  
  - `udp.dstport == 53` to isolate DNS query traffic to port 53.  
- **Description:**  
  Captures domain name lookup requests and associated responses from DNS servers.  
  Helps analyze DNS activity and detect anomalous query patterns.

### HTTP Traffic & Credentials
- **Filters:**
- 
  - `tcp.port == 80` to show all HTTP traffic.  
  - `tcp.stream eq <stream_number>` to follow the full TCP stream for a session (e.g., 76).  
- **Description:**  
  View HTTP GET and POST requests including potential exposure of credentials in plaintext HTTP traffic.  
  The "Follow TCP Stream" tool reconstructs entire session traffic for detailed analysis.

### TCP Traffic & Security Analysis
- **Filters:**
- 
  - `tcp.srcport == 443` to display HTTPS (TLS) traffic.  
  - `tcp.flags.syn == 1 and tcp.flags.ack == 0` for detecting TCP SYN packets, often used to identify SYN flood DoS attempts.  
- **Description:**  
  Analysis of encrypted traffic streams and detection of suspicious packet flood patterns.

## Summary Table

| Protocol | Filter Used                         | Purpose                               |
|----------|-----------------------------------|-------------------------------------|
| ARP      | `arp`                             | IP-MAC address resolution            |
| DNS      | `ip.src == <host_ip>`             | Source-specific host traffic         |
| DNS      | `udp.dstport == 53`               | DNS query capture                    |
| HTTP     | `tcp.port == 80`                  | Web browsing traffic                 |
| HTTP     | `tcp.stream eq <stream>`          | Full HTTP session reconstruction    |
| TCP      | `tcp.srcport == 443`              | HTTPS traffic                       |
| TCP SYN  | `tcp.flags.syn == 1 and tcp.flags.ack == 0` | Detection of SYN flood attack patterns |

## Usage Guidelines
1. Open the `.pcapng` capture file in Wireshark.
2. Apply filters listed above in the Wireshark filter bar.
3. Examine packet lists, protocol details pane, and follow TCP streams as needed.
4. Use screenshots as visual references for filter application and packet inspection.

## Screenshots Included
Screenshots visually demonstrate:
- ARP request and reply packets filtered by `arp`.
- DNS query traffic filtered by IP and port.
- HTTP traffic and credential capture by following TCP streams.
- TCP port filtering and detection of DoS-related SYN flood traffic.

---

This repository serves as a comprehensive resource for learning to capture and analyze network traffic using Wireshark, highlighting practical cybersecurity analysis steps and protocol-specific insights.

