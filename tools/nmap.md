# Nmap

Nmap (Network Mapper) is an open-source tool for network discovery, port scanning, service enumeration, and security auditing.

Personal notes and reference for Nmap options and commands.

---

## Target Specification

| Option | Description |
|---|---|
| `<target>` | Scan a single target |
| `-iL <file>` | Scan targets from a file |
| `-iR <num>` | Scan random targets |
| `--exclude <targets>` | Exclude targets |
| `--excludefile <file>` | Exclude targets listed in a file |

---

## Host Discovery

| Option | Description |
|---|---|
| `-sL` | List targets without scanning |
| `-sn` | Host discovery only, no port scan |
| `-Pn` | Skip host discovery |
| `-PS` | TCP SYN ping |
| `-PA` | TCP ACK ping |
| `-PU` | UDP ping |
| `-PE` | ICMP echo request |
| `-PP` | ICMP timestamp request |
| `-PM` | ICMP address mask request |
| `-PR` | ARP discovery |
| `-n` | Disable DNS resolution |
| `-R` | Always resolve DNS |

---

## Port Scanning

| Option | Description |
|---|---|
| `-p <ports>` | Scan specific ports |
| `-p-` | Scan all 65,535 TCP ports |
| `-F` | Fast scan, fewer ports |
| `--top-ports <num>` | Scan most common ports |
| `-r` | Scan ports sequentially |
| `--exclude-ports <ports>` | Exclude ports |

### Port ranges

| Syntax | Description |
|---|---|
| `-p 22` | Single port |
| `-p 22,80,443` | Multiple ports |
| `-p 1-1000` | Port range |
| `-p-` | All ports |
| `-p U:53,T:80` | UDP 53 + TCP 80 |

---

## Scan Techniques

| Option | Description |
|---|---|
| `-sS` | TCP SYN scan |
| `-sT` | TCP Connect scan |
| `-sU` | UDP scan |
| `-sA` | TCP ACK scan |
| `-sW` | TCP Window scan |
| `-sM` | TCP Maimon scan |
| `-sN` | TCP Null scan |
| `-sF` | TCP FIN scan |
| `-sX` | TCP Xmas scan |
| `-sY` | SCTP INIT scan |
| `-sZ` | SCTP COOKIE-ECHO scan |
| `-sO` | IP protocol scan |

`-sS` is one of the most commonly used TCP scan types.

---

## Service & Version Detection

| Option | Description |
|---|---|
| `-sV` | Service/version detection |
| `--version-intensity <0-9>` | Version detection intensity |
| `--version-light` | Reduce version detection intensity |
| `--version-all` | Try every version probe |
| `--version-trace` | Show detailed version detection activity |

---

## OS Detection

| Option | Description |
|---|---|
| `-O` | OS detection |
| `--osscan-limit` | Limit OS detection to promising targets |
| `--osscan-guess` | Guess OS more aggressively |
| `--max-os-tries <num>` | Maximum OS detection attempts |

---

## NSE

**Nmap Scripting Engine**

| Option | Description |
|---|---|
| `-sC` | Run default NSE scripts |
| `--script <scripts>` | Run specified scripts |
| `--script=<category>` | Run scripts from a category |
| `--script-help <scripts>` | Show script information |
| `--script-args <args>` | Provide script arguments |
| `--script-trace` | Show script communication |
| `--script-updatedb` | Update NSE script database |

### Common NSE categories

`auth` · `broadcast` · `brute` · `default` · `discovery` · `dos` · `exploit` · `external` · `fuzzer` · `intrusive` · `malware` · `safe` · `version` · `vuln`

---

## Timing & Performance

| Option | Description |
|---|---|
| `-T0` | Paranoid |
| `-T1` | Sneaky |
| `-T2` | Polite |
| `-T3` | Normal (default) |
| `-T4` | Aggressive |
| `-T5` | Insane |
| `--min-rate <num>` | Minimum packet sending rate |
| `--max-rate <num>` | Maximum packet sending rate |
| `--min-parallelism <num>` | Minimum probe parallelism |
| `--max-parallelism <num>` | Maximum probe parallelism |
| `--host-timeout <time>` | Give up on a target after a timeout |
| `--scan-delay <time>` | Minimum delay between probes |
| `--max-scan-delay <time>` | Maximum delay between probes |

Higher timing values increase speed but can reduce reliability and increase network traffic.

---

## Firewall / IDS Evasion

| Option | Description |
|---|---|
| `-f` | Fragment packets |
| `-D <decoys>` | Use decoy IP addresses |
| `-S <IP>` | Spoof source IP |
| `-e <interface>` | Specify network interface |
| `-g <port>` | Use a specific source port |
| `--source-port <port>` | Specify source port |
| `--proxies <url>` | Relay through HTTP/SOCKS proxies |
| `--data <hex>` | Append custom payload |
| `--data-string <text>` | Append custom ASCII data |
| `--ttl <value>` | Set IP time-to-live |

> These options are mainly relevant for controlled security testing and evasion research.

---

## Output

| Option | Description |
|---|---|
| `-oN <file>` | Normal output |
| `-oX <file>` | XML output |
| `-oG <file>` | Grepable output |
| `-oS <file>` | Script kiddie output |
| `-oA <name>` | Output in multiple formats |
| `-v` | Increase verbosity |
| `-vv` | More verbose output |
| `-d` | Increase debugging |
| `-dd` | More debugging |
| `--reason` | Show reason for port state |
| `--open` | Show only open/possibly open ports |
| `--packet-trace` | Show packets sent and received |

---

## DNS

| Option | Description |
|---|---|
| `-n` | Disable DNS resolution |
| `-R` | Always perform DNS resolution |
| `--dns-servers <servers>` | Use specific DNS servers |
| `--system-dns` | Use the system DNS resolver |

---

## IPv4 / IPv6 Protocols

| Option | Description |
|---|---|
| `-4` | IPv4 |
| `-6` | IPv6 |

---

## Input / Output & Miscellaneous

| Option | Description |
|---|---|
| `-A` | Enable OS detection, version detection, default scripts and traceroute |
| `-sV` | Service/version detection |
| `--traceroute` | Trace route to host |
| `--reason` | Explain why a port has its state |
| `--open` | Only show open/possibly open ports |
| `-n` | No DNS resolution |
| `-6` | IPv6 scanning |
| `-V` | Display Nmap version |
| `-h` | Show help |

---

## Common Combinations

| Command | Purpose |
|---|---|
| `nmap <target>` | Basic scan |
| `nmap -p- <target>` | All TCP ports |
| `nmap -sV <target>` | Service/version detection |
| `nmap -sC <target>` | Default NSE scripts |
| `nmap -sC -sV <target>` | Scripts + versions |
| `nmap -O <target>` | OS detection |
| `nmap -A <target>` | Aggressive scan |
| `nmap -Pn <target>` | Skip host discovery |
| `nmap -sU <target>` | UDP scan |
| `nmap -T4 <target>` | Faster timing |
| `nmap --top-ports <num> <target>` | Most common ports |
| `nmap -oA <name> <target>` | Save in multiple formats |

---

## Port States

| State | Meaning |
|---|---|
| `open` | A service is listening |
| `closed` | Port is reachable but no service is listening |
| `filtered` | Filtering prevents Nmap from determining the state |
| `unfiltered` | Port is accessible but its open/closed state cannot be determined |
| `open\|filtered` | Nmap cannot determine whether it is open or filtered |
| `closed\|filtered` | Nmap cannot determine whether it is closed or filtered |

---

## Notes

- `-sV` identifies services and versions.
- `-sC` runs the default NSE scripts.
- `-Pn` skips host discovery.
- `-p-` scans all TCP ports.
- `-O` attempts OS detection.
- `-A` enables several advanced detection features.
- `-T4` / `-T5` increase scanning speed.
- `-oA` is useful for keeping scan results in several formats.
- A `?` after a detected service means Nmap is not completely confident about the identification.
- `sudo` is often required for scans that use raw packets or privileged features.

---

## Resources

- [Nmap Reference Guide](https://nmap.org/book/man.html)
- [Nmap Network Scanning](https://nmap.org/book/)
- [Nmap NSE Documentation](https://nmap.org/nsedoc/)
