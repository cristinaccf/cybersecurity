# Netcat

Netcat (`nc`) is a networking utility for reading from and writing to network connections using TCP or UDP.

It is commonly used for network troubleshooting, service enumeration, port testing, banner grabbing, data transfer, and shell communication.

Personal notes and reference for using Netcat in cybersecurity labs and CTFs.

---

# Basic Syntax

```bash
nc [options] <target> <port>
```

---

# TCP Connections

### Connect to a TCP service

```text
nc <TARGET> <PORT>
```

Used to connect to an open TCP port.

### Specify a source port

```text
nc -p <PORT> <TARGET> <PORT>
```

---

# UDP

### UDP connection

```text
nc -u <TARGET> <PORT>
```

`-u` switches Netcat from TCP to UDP.

---

# Listening

### Listen on a TCP port

```text
nc -lvnp <PORT>
```

| Option | Description |
|---|---|
| `-l` | Listen mode |
| `-v` | Verbose |
| `-n` | Do not resolve DNS |
| `-p` | Local port |

Useful for receiving connections from another host.

---

# Port Checking

Netcat can be used to test whether a port accepts connections.

```text
nc -zv <TARGET> <PORT>
```

| Option | Description |
|---|---|
| `-z` | Zero-I/O mode |
| `-v` | Verbose |

### Port range

```text
nc -zv <TARGET> <START>-<END>
```

Useful for quick connectivity checks.

---

# Banner Grabbing

Connect directly to a service:

```text
nc <TARGET> <PORT>
```

Some services return a banner containing information such as:

- Service name
- Version
- Operating system
- Protocol information

Useful for basic service enumeration.

---

# File Transfer

Netcat can transfer data between two systems.

### Receiver

```text
nc -lvnp <PORT> > file
```

### Sender

```text
nc <TARGET> <PORT> < file
```

The receiving side must be listening before the sender connects.

---

# Reverse Shell

Netcat can be used to establish a reverse shell in authorized lab environments.

### Listener

```text
nc -lvnp <PORT>
```

The target connects back to the listener.

The exact reverse-shell command depends on the target operating system and available shell.

> Only use reverse shells on systems where you have explicit authorization.

---

# Bind Shell

In a bind shell, the target listens for an incoming connection.

Conceptually:

```text
Attacker → Target
```

This differs from a reverse shell:

```text
Target → Attacker
```

---

# File / Data Transfer Modes

Netcat can send arbitrary data through a TCP connection.

```text
Sender → nc → Network → nc → Receiver
```

Useful for:

- Simple file transfers
- Testing connectivity
- Sending raw data
- Receiving command output

---

# Common Options

| Option | Description |
|---|---|
| `-l` | Listen mode |
| `-v` | Verbose |
| `-vv` | More verbose |
| `-n` | Disable DNS resolution |
| `-p <port>` | Specify local port |
| `-u` | UDP mode |
| `-z` | Zero-I/O port scanning |
| `-w <seconds>` | Connection timeout |
| `-k` | Keep listening after a connection |
| `-q <seconds>` | Quit after EOF |
| `-s <IP>` | Specify local source address |

---

# Useful Combinations

| Command | Purpose |
|---|---|
| `nc <TARGET> <PORT>` | Connect to a TCP service |
| `nc -u <TARGET> <PORT>` | Connect using UDP |
| `nc -lvnp <PORT>` | Listen on a TCP port |
| `nc -zv <TARGET> <PORT>` | Check a TCP port |
| `nc -zv <TARGET> <START>-<END>` | Check a port range |
| `nc -lvnp <PORT> > file` | Receive data/file |
| `nc <TARGET> <PORT> < file` | Send data/file |

---

# TCP vs UDP

| Protocol | Characteristics |
|---|---|
| **TCP** | Connection-oriented, reliable |
| **UDP** | Connectionless, faster, no delivery guarantee |

Use:

```text
nc <TARGET> <PORT>
```

for TCP.

Use:

```text
nc -u <TARGET> <PORT>
```

for UDP.

---

# Troubleshooting

Useful options when diagnosing connections:

```text
-v
-vv
-n
-w
```

Things to check:

- Target IP
- Port number
- TCP vs UDP
- Firewall rules
- Listener status
- Network connectivity
- Service availability

---

# Common HTB Uses

```text
Service enumeration
Banner grabbing
Port connectivity testing
Receiving connections
Sending connections
File transfers
Reverse shells
Bind shells
Network troubleshooting
```

---

# Notes

- Netcat does not automatically understand application protocols. It simply sends and receives data.
- It can be useful for manually interacting with services discovered by Nmap.
- `-z` is useful for checking port connectivity without sending application data.
- `-n` avoids DNS lookups.
- `-v` helps understand what is happening.
- Netcat implementations can differ. OpenBSD `nc`, traditional Netcat, and Ncat may support different options.
- For encrypted services such as HTTPS, plain Netcat does not perform TLS negotiation.

---

## Resources

- [Ncat Documentation](https://nmap.org/ncat/)
- [Nmap Project](https://nmap.org/)
