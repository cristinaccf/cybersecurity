# ffuf

ffuf (Fuzz Faster U Fool) is a fast web fuzzer written in Go.

It can be used for directory and file discovery, virtual host discovery, parameter fuzzing, and other HTTP enumeration tasks.

Personal notes and reference for using ffuf in cybersecurity labs and CTFs.

---

## Basic Syntax

```bash
ffuf [options]
```

The keyword `FUZZ` marks the position where ffuf inserts values from the wordlist.

---

# URL / Directory Fuzzing

```text
-u <URL>
```

Target URL.

```text
-w <wordlist>
```

Wordlist used for fuzzing.

Common locations on Kali:

```text
/usr/share/seclists/
/usr/share/wordlists/
```

### Common options

| Option | Description |
|---|---|
| `-u` | Target URL |
| `-w` | Wordlist |
| `-t` | Number of threads |
| `-o` | Output file |
| `-of` | Output format |
| `-e` | File extensions |
| `-r` | Follow redirects |
| `-recursion` | Enable recursion |
| `-recursion-depth` | Maximum recursion depth |
| `-s` | Silent mode |
| `-v` | Verbose output |
| `-c` | Colorize output |
| `-ac` | Automatically calibrate filtering |

---

# Matchers

Matchers determine which responses are considered interesting.

| Option | Description |
|---|---|
| `-mc` | Match HTTP status codes |
| `-ml` | Match response line count |
| `-mw` | Match response word count |
| `-ms` | Match response size |
| `-mt` | Match response time |

Example values:

```text
-mc 200,204,301,302,307,401,403
```

Default matching behavior can be changed depending on the target.

---

# Filters

Filters remove unwanted results from the output.

| Option | Description |
|---|---|
| `-fc` | Filter status codes |
| `-fl` | Filter line count |
| `-fw` | Filter word count |
| `-fs` | Filter response size |
| `-ft` | Filter response time |
| `-fr` | Filter regular expression |

Filtering is especially useful when the server returns the same response for non-existent resources.

---

# File Extensions

Use `-e` to test multiple file extensions.

```text
-e .php,.txt,.html,.bak
```

Useful extensions can include:

```text
.php
.txt
.html
.htm
.bak
.old
.zip
.tar.gz
.conf
.config
```

The extensions should depend on the technology being tested.

---

# HTTP Methods

```text
-X <METHOD>
```

Specify the HTTP method.

Common methods:

```text
GET
POST
PUT
PATCH
DELETE
HEAD
OPTIONS
```

Useful when testing APIs or endpoints that behave differently depending on the HTTP method.

---

# Headers

### Custom header

```text
-H "<HEADER>: <VALUE>"
```

Useful headers include:

```text
Host
Authorization
Cookie
Content-Type
User-Agent
X-Forwarded-For
```

---

# Cookies

```text
-b "<COOKIE>"
```

Used to send cookies with requests.

Useful when fuzzing authenticated areas of an application.

---

# User-Agent

```text
-H "User-Agent: <VALUE>"
```

Can be used to test how a server responds to different clients.

---

# Request Data

### POST data

```text
-d "<DATA>"
```

Used to send data in the request body.

### Content-Type

```text
-H "Content-Type: application/x-www-form-urlencoded"
```

or:

```text
-H "Content-Type: application/json"
```

Useful for parameter and API fuzzing.

---

# Parameter Fuzzing

Fuzz parameters by placing `FUZZ` where the value should be inserted.

Example locations:

```text
?id=FUZZ
```

```text
?file=FUZZ
```

```text
?search=FUZZ
```

```text
-X POST -d "username=FUZZ"
```

Useful for discovering hidden values, parameters, or application behavior.

---

# Multiple Wordlists

ffuf supports multiple wordlists using different keywords.

```text
-w users.txt:USER
-w passwords.txt:PASS
```

Then use:

```text
USER
PASS
```

as placeholders in the request.

This can be useful for testing combinations of values.

---

# Virtual Host / Host Header Fuzzing

The `Host` header can be fuzzed to discover virtual hosts.

```text
-H "Host: FUZZ.<DOMAIN>"
```

Useful for discovering applications hosted on different virtual hosts.

---

# Subdomain Fuzzing

Fuzz the subdomain portion of the URL:

```text
https://FUZZ.<DOMAIN>
```

This can be used to discover subdomains when DNS and web configuration allow it.

---

# Response Filtering

One of the most important parts of ffuf is learning to distinguish real results from false positives.

Useful filters:

```text
-fc <status>
-fs <size>
-fw <words>
-fl <lines>
-fr <regex>
```

Example concepts:

```text
200 + unusual size → potentially interesting
403 → resource may exist but access is restricted
404 → usually not found
Same size across many responses → possible wildcard/default response
```

---

# Calibration

### `-ac`

Automatically calibrates the filtering options.

```text
-ac
```

Useful when the web server returns custom responses for nonexistent resources.

---

# Recursion

### `-recursion`

Enable recursive scanning.

```text
-recursion
```

### `-recursion-depth`

Limit recursion depth.

```text
-recursion-depth <depth>
```

Useful for automatically discovering directories inside discovered directories.

---

# Proxy

### `-x`

Use an HTTP/SOCKS proxy.

```text
-x <proxy>
```

Useful when routing traffic through tools such as Burp Suite.

---

# TLS / HTTPS

### `-k`

Ignore TLS certificate validation.

Useful when the target uses a self-signed or invalid certificate.

---

# Rate & Performance

| Option | Description |
|---|---|
| `-t` | Number of threads |
| `-rate` | Requests per second |
| `-p` | Delay between requests |
| `-timeout` | HTTP request timeout |
| `-maxtime` | Maximum runtime |
| `-maxtime-job` | Maximum runtime per job |

Higher concurrency increases speed but also increases traffic.

---

# Output

| Option | Description |
|---|---|
| `-o <file>` | Output file |
| `-of <format>` | Output format |
| `-s` | Silent mode |
| `-v` | Verbose output |
| `-c` | Colorized output |

Common output formats:

```text
json
ejson
html
md
csv
ecsv
all
```

---

# Useful Options

| Option | Description |
|---|---|
| `-u` | Target URL |
| `-w` | Wordlist |
| `-t` | Threads |
| `-e` | Extensions |
| `-mc` | Match status codes |
| `-fc` | Filter status codes |
| `-fs` | Filter response size |
| `-fw` | Filter response words |
| `-fl` | Filter response lines |
| `-fr` | Filter by regex |
| `-H` | Custom header |
| `-b` | Cookies |
| `-X` | HTTP method |
| `-d` | POST data |
| `-r` | Follow redirects |
| `-ac` | Auto-calibration |
| `-recursion` | Recursive scanning |
| `-k` | Ignore TLS errors |
| `-x` | Proxy |
| `-o` | Output file |
| `-of` | Output format |
| `-s` | Silent mode |
| `-v` | Verbose mode |
| `-rate` | Requests per second |
| `-timeout` | Request timeout |

---

# Common Fuzzing Locations

```text
Directories:
https://<TARGET>/FUZZ

Files:
https://<TARGET>/FUZZ.php

Extensions:
https://<TARGET>/FUZZ

Parameters:
https://<TARGET>/?FUZZ=value

Parameter values:
https://<TARGET>/?id=FUZZ

POST parameters:
username=FUZZ&password=test

Virtual hosts:
Host: FUZZ.<DOMAIN>

Subdomains:
https://FUZZ.<DOMAIN>
```

---

# Common Workflow

```text
1. Identify the web application
2. Choose an appropriate wordlist
3. Fuzz directories/files
4. Test relevant extensions
5. Analyze status codes and response sizes
6. Filter false positives
7. Fuzz parameters when appropriate
8. Enumerate virtual hosts/subdomains
9. Investigate interesting results
10. Repeat with different wordlists if necessary
```

---

# Notes

- `FUZZ` is the placeholder used by ffuf.
- Matchers (`-mc`, `-ms`, `-mw`, etc.) identify interesting responses.
- Filters (`-fc`, `-fs`, `-fw`, etc.) remove unwanted responses.
- Response size is often useful for identifying false positives.
- `-ac` can help when the server returns similar responses for invalid paths.
- Wordlist selection has a large impact on enumeration results.
- Use recursion carefully on large applications.
- Higher thread counts generate more traffic.
- Always perform fuzzing only against systems you are authorized to test.

---

## Resources

- [ffuf GitHub](https://github.com/ffuf/ffuf)
- [SecLists](https://github.com/danielmiessler/SecLists)
