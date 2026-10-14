# Gobuster

Gobuster is a tool written in Go that is used for directory/file enumeration, DNS enumeration, virtual host discovery, and other forms of brute-force enumeration.

Personal notes and reference for using Gobuster in cybersecurity labs and CTFs.

---

## Basic Syntax

```bash
gobuster <mode> [options]
```

Common modes:

```text
dir
dns
vhost
fuzz
s3
gcs
tftp
```

---

# Directory & File Enumeration

## `dir`

Used to discover directories and files on web servers.

```bash
gobuster dir -u <URL> -w <WORDLIST>
```

### Common Options

| Option | Description |
|---|---|
| `-u` | Target URL |
| `-w` | Wordlist |
| `-t` | Number of concurrent threads |
| `-o` | Output file |
| `-x` | File extensions to search |
| `-s` | Positive status codes |
| `-b` | Status codes to exclude |
| `-r` | Follow redirects |
| `-k` | Skip TLS certificate verification |
| `-q` | Quiet mode |
| `-v` | Verbose output |
| `-n` | Hide status code |
| `--no-error` | Don't display errors |
| `--timeout` | HTTP request timeout |
| `--delay` | Delay between requests |
| `-a` | User-Agent |
| `-H` | Custom HTTP header |
| `-c` | Cookies |

### File Extensions

```bash
-x php,txt,html,bak
```

Useful when looking for files such as:

```text
.php
.txt
.html
.bak
.zip
.conf
```

---

# DNS Enumeration

## `dns`

Used to discover subdomains through DNS brute-forcing.

```bash
gobuster dns -d <DOMAIN> -w <WORDLIST>
```

### Common Options

| Option | Description |
|---|---|
| `-d` | Target domain |
| `-w` | Wordlist |
| `-t` | Threads |
| `-o` | Output file |
| `-i` | Show IP addresses |
| `-r` | DNS resolver |
| `-c` | Show CNAME records |
| `-q` | Quiet mode |

### Useful DNS options

```bash
-i
```

Show the IP address associated with discovered subdomains.

```bash
-r <DNS_SERVER>
```

Use a specific DNS resolver.

---

# Virtual Host Enumeration

## `vhost`

Used to discover virtual hosts configured on a web server.

```bash
gobuster vhost -u <URL> -w <WORDLIST>
```

### Common Options

| Option | Description |
|---|---|
| `-u` | Target URL |
| `-w` | Wordlist |
| `-t` | Threads |
| `-o` | Output file |
| `--append-domain` | Append domain to words |
| `--exclude-length` | Exclude responses by body length |
| `-r` | Follow redirects |
| `-k` | Skip TLS certificate verification |
| `-a` | User-Agent |
| `-H` | Custom HTTP header |
| `-c` | Cookies |

VHost enumeration can reveal applications that are not directly accessible through the main domain.

---

# Fuzzing

## `fuzz`

Used to fuzz URLs, parameters, headers, or other parts of HTTP requests.

```bash
gobuster fuzz -u <URL> -w <WORDLIST>
```

The `FUZZ` keyword indicates where the wordlist values are inserted.

```text
FUZZ
```

### Common Options

| Option | Description |
|---|---|
| `-u` | Target URL |
| `-w` | Wordlist |
| `-t` | Threads |
| `-o` | Output file |
| `-s` | Positive status codes |
| `-b` | Excluded status codes |
| `--exclude-length` | Exclude responses by body length |
| `-r` | Follow redirects |
| `-k` | Skip TLS verification |
| `-H` | Custom HTTP header |
| `-c` | Cookies |
| `-a` | User-Agent |

---

# S3 Enumeration

## `s3`

Used to enumerate Amazon S3 buckets.

```bash
gobuster s3 -w <WORDLIST>
```

### Common Options

| Option | Description |
|---|---|
| `-w` | Wordlist |
| `-t` | Threads |
| `-o` | Output file |
| `-q` | Quiet mode |

---

# Google Cloud Storage

## `gcs`

Used to enumerate Google Cloud Storage buckets.

```bash
gobuster gcs -w <WORDLIST>
```

---

# TFTP

## `tftp`

Used for TFTP enumeration.

```bash
gobuster tftp -u <TARGET> -w <WORDLIST>
```

Useful options include:

| Option | Description |
|---|---|
| `-u` | Target |
| `-w` | Wordlist |
| `-t` | Threads |
| `-o` | Output file |

---

# Wordlists

Gobuster relies heavily on wordlists.

Common locations on Kali:

```text
/usr/share/wordlists/
/usr/share/seclists/
```

Useful SecLists directories:

```text
Discovery/
Discovery/Web-Content/
Discovery/DNS/
Fuzzing/
Passwords/
Usernames/
```

Common wordlists include:

```text
directory-list-2.3-medium.txt
directory-list-2.3-big.txt
common.txt
```

For web enumeration, **SecLists** is one of the most useful collections of wordlists.

---

# HTTP Status Codes

Gobuster commonly uses HTTP status codes to determine which results are interesting.

| Code | Meaning |
|---|---|
| `200` | OK |
| `201` | Created |
| `204` | No Content |
| `301` | Permanent Redirect |
| `302` | Temporary Redirect |
| `307` | Temporary Redirect |
| `401` | Unauthorized |
| `403` | Forbidden |
| `404` | Not Found |
| `405` | Method Not Allowed |
| `500` | Internal Server Error |

A `403` response can still be interesting because the resource exists but access is restricted.

---

# Threads & Performance

### `-t`

Controls the number of concurrent threads.

```text
-t <number>
```

Higher values increase speed but also increase traffic and resource usage.

### `--delay`

Adds a delay between requests.

```text
--delay <duration>
```

### `--timeout`

Controls the HTTP request timeout.

```text
--timeout <duration>
```

---

# Output

### Save output

```text
-o <file>
```

### Quiet mode

```text
-q
```

Only display relevant results.

### Verbose mode

```text
-v
```

Display additional information.

---

# HTTPS

### Ignore TLS certificate errors

```text
-k
```

Useful when testing HTTPS services with self-signed or invalid certificates.

---

# Headers & Cookies

### Custom header

```text
-H "<HEADER>: <VALUE>"
```

### Cookies

```text
-c "<COOKIE>=<VALUE>"
```

### User-Agent

```text
-a "<USER-AGENT>"
```

Useful when a web application behaves differently depending on headers or authentication state.

---

# Useful Options

| Option | Description |
|---|---|
| `-u` | Target URL |
| `-w` | Wordlist |
| `-t` | Threads |
| `-o` | Output file |
| `-x` | File extensions |
| `-s` | Include status codes |
| `-b` | Exclude status codes |
| `-k` | Ignore TLS certificate errors |
| `-r` | Follow redirects |
| `-q` | Quiet mode |
| `-v` | Verbose mode |
| `-H` | Custom HTTP header |
| `-c` | Cookies |
| `-a` | User-Agent |
| `--exclude-length` | Exclude responses by body length |
| `--timeout` | Request timeout |
| `--delay` | Delay between requests |

---

# Common Commands

| Command | Purpose |
|---|---|
| `gobuster dir` | Directory/file enumeration |
| `gobuster dns` | DNS/subdomain enumeration |
| `gobuster vhost` | Virtual host enumeration |
| `gobuster fuzz` | HTTP fuzzing |
| `gobuster s3` | S3 bucket enumeration |
| `gobuster gcs` | Google Cloud Storage enumeration |
| `gobuster tftp` | TFTP enumeration |

---

# Enumeration Workflow

A common web enumeration workflow:

```text
1. Identify the web server
2. Enumerate directories
3. Enumerate files/extensions
4. Enumerate subdomains
5. Enumerate virtual hosts
6. Investigate interesting responses
7. Repeat with different wordlists when necessary
```

---

# Notes

- Choose the wordlist according to the target.
- A larger wordlist is not always better.
- Pay attention to `200`, `301`, `302`, `401`, and `403` responses.
- Compare response lengths when many results return the same status code.
- `403 Forbidden` can still indicate an interesting resource.
- HTTPS targets may require `-k` when using invalid/self-signed certificates.
- Increase threads carefully.
- Always perform enumeration only against systems you are authorized to test.

---

## Resources

- [Gobuster GitHub](https://github.com/OJ/gobuster)
- [SecLists](https://github.com/danielmiessler/SecLists)
