# Wireshark

Wireshark is a network protocol analyzer used to capture, inspect, and analyze network traffic.

It is useful for understanding protocols, troubleshooting networks, analyzing PCAP files, and investigating security incidents.

Personal notes and reference for using Wireshark in cybersecurity labs and CTFs.

---

# Capture

## Interfaces

Select the network interface from which traffic should be captured.

Common interfaces:

```text
eth0
wlan0
lo
tun0
```

`tun0` is commonly used for VPN connections such as Hack The Box.

---

# Capture Filters

Capture filters determine **what traffic is captured**.

They use Berkeley Packet Filter (BPF) syntax.

| Filter | Description |
|---|---|
| `host <IP>` | Traffic to/from a host |
| `src host <IP>` | Traffic from a host |
| `dst host <IP>` | Traffic to a host |
| `port <PORT>` | Traffic using a port |
| `src port <PORT>` | Traffic from a port |
| `dst port <PORT>` | Traffic to a port |
| `tcp` | TCP traffic |
| `udp` | UDP traffic |
| `icmp` | ICMP traffic |
| `arp` | ARP traffic |
| `dns` | DNS traffic |

### Combining filters

| Operator | Meaning |
|---|---|
| `and` / `&&` | Both conditions |
| `or` / `||` | Either condition |
| `not` / `!` | Negation |

---

# Display Filters

Display filters are applied **after traffic has been captured**.

They are more powerful than capture filters.

## Common filters

| Filter | Description |
|---|---|
| `ip.addr == <IP>` | Traffic to/from IP |
| `ip.src == <IP>` | Source IP |
| `ip.dst == <IP>` | Destination IP |
| `tcp.port == <PORT>` | TCP port |
| `udp.port == <PORT>` | UDP port |
| `tcp` | TCP traffic |
| `udp` | UDP traffic |
| `icmp` | ICMP traffic |
| `arp` | ARP traffic |
| `dns` | DNS traffic |
| `http` | HTTP traffic |
| `tls` | TLS traffic |
| `ssh` | SSH traffic |
| `ftp` | FTP traffic |
| `smb` | SMB traffic |

---

# HTTP

Useful filters:

```text
http
http.request
http.response
http.request.method
http.request.uri
http.host
http.user_agent
http.cookie
http.authorization
```

Useful information:

- HTTP methods
- URLs
- Host headers
- Parameters
- Cookies
- User-Agent
- Authorization headers
- Server responses

---

# DNS

Useful filters:

```text
dns
dns.qry.name
dns.qry.type
dns.flags.response
dns.a
dns.aaaa
```

Useful information:

- Queried domains
- DNS responses
- IP addresses
- Record types
- Potentially suspicious domains

---

# TCP

Useful filters:

```text
tcp
tcp.port == <PORT>
tcp.stream
tcp.flags
tcp.flags.syn == 1
tcp.flags.ack == 1
tcp.flags.fin == 1
tcp.flags.reset == 1
```

TCP flags:

| Flag | Meaning |
|---|---|
| `SYN` | Start connection |
| `ACK` | Acknowledge data |
| `FIN` | Finish connection |
| `RST` | Reset connection |
| `PSH` | Push data |
| `URG` | Urgent data |

---

# UDP

Useful filters:

```text
udp
udp.port == <PORT>
```

UDP is connectionless and does not use TCP-style connection flags.

---

# ICMP

Useful filters:

```text
icmp
icmp.type
icmp.code
```

Useful for analyzing:

- Ping
- Network reachability
- ICMP errors
- Network diagnostics

---

# ARP

Useful filters:

```text
arp
arp.opcode
arp.src.proto_ipv4
arp.dst.proto_ipv4
```

Useful for investigating:

- MAC/IP mappings
- ARP requests
- ARP replies
- ARP spoofing

---

# Follow Streams

Wireshark can reconstruct application conversations.

Available options include:

```text
Follow → TCP Stream
Follow → UDP Stream
Follow → HTTP Stream
```

Useful for viewing the complete conversation between endpoints.

---

# Statistics

Useful Wireshark statistics:

```text
Statistics → Protocol Hierarchy
Statistics → Conversations
Statistics → Endpoints
Statistics → I/O Graphs
Statistics → Flow Graph
```

These can help identify:

- Most-used protocols
- Communicating hosts
- Traffic volume
- Network relationships
- Suspicious connections

---

# Endpoints

The Endpoints view shows discovered network endpoints.

Useful for identifying:

- Source IPs
- Destination IPs
- MAC addresses
- IPv4/IPv6 hosts

---

# Conversations

The Conversations view shows communication pairs.

Useful for identifying:

- Who is communicating
- Which ports are being used
- Amount of traffic
- Duration of communication

---

# Protocol Hierarchy

Shows a breakdown of protocols present in the capture.

Useful for quickly understanding what types of traffic are present.

Example hierarchy:

```text
Ethernet
└── IPv4
    ├── TCP
    │   └── HTTP
    └── UDP
        └── DNS
```

---

# PCAP Analysis

Wireshark can open packet capture files such as:

```text
.pcap
.pcapng
```

When analyzing a PCAP, look for:

- Interesting IP addresses
- Open connections
- DNS queries
- HTTP requests
- Authentication attempts
- Cleartext credentials
- File transfers
- Suspicious protocols
- Unusual traffic patterns

---

# Export Objects

Wireshark can extract objects transferred through supported protocols.

Useful for:

- HTTP files
- Images
- Documents
- Other transferred data

Menu:

```text
File → Export Objects
```

---

# Name Resolution

Wireshark can resolve addresses into names.

Useful settings:

```text
View → Name Resolution
```

DNS resolution can make captures easier to understand, but it can also generate additional DNS traffic during live analysis.

---

# Encryption

Encrypted protocols may hide application content.

Common encrypted protocols:

```text
HTTPS
TLS
SSH
SFTP
```

Even when payload contents are encrypted, metadata can still reveal:

- Source/destination IP
- Ports
- Timing
- Packet sizes
- TLS information
- Certificate information

---

# Useful Filters

### Find a specific IP

```text
ip.addr == <IP>
```

### Find a specific port

```text
tcp.port == <PORT>
```

### Find HTTP POST requests

```text
http.request.method == "POST"
```

### Find HTTP GET requests

```text
http.request.method == "GET"
```

### Find DNS queries

```text
dns.qry.name
```

### Find TCP SYN packets

```text
tcp.flags.syn == 1
```

### Find TCP resets

```text
tcp.flags.reset == 1
```

### Find a specific host communicating with another

```text
ip.src == <SOURCE> && ip.dst == <DESTINATION>
```

---

# Useful Features

| Feature | Purpose |
|---|---|
| **Capture** | Record network traffic |
| **Display Filters** | Filter captured traffic |
| **Follow Stream** | Reconstruct conversations |
| **Statistics** | Analyze traffic patterns |
| **Endpoints** | Identify hosts |
| **Conversations** | Analyze communication pairs |
| **Protocol Hierarchy** | Identify protocols |
| **Export Objects** | Extract transferred files |
| **Packet Details** | Inspect protocol fields |
| **Packet Bytes** | View raw packet data |

---

# Common Workflow

```text
1. Select interface or open a PCAP
2. Capture or load traffic
3. Identify protocols
4. Identify communicating hosts
5. Filter interesting traffic
6. Follow relevant streams
7. Inspect packet details
8. Extract useful information
9. Export objects when appropriate
10. Document findings
```

---

# Notes

- **Capture filters** determine what traffic is captured.
- **Display filters** filter traffic that has already been captured.
- `Follow TCP Stream` is extremely useful when investigating application traffic.
- Encrypted traffic can still reveal metadata even when the payload cannot be read.
- PCAP analysis is useful for both troubleshooting and security investigations.
- Wireshark can dissect hundreds of network protocols.
- Large captures are easier to analyze by starting with hosts, protocols, and ports of interest.

---

## Resources

- [Wireshark Documentation](https://www.wireshark.org/docs/)
- [Wireshark Display Filter Reference](https://www.wireshark.org/docs/dfref/)
