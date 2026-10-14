# Burp Suite

Burp Suite is a web application security testing platform used to intercept, inspect, modify, and replay HTTP/HTTPS traffic.

Personal notes and reference for web application testing and cybersecurity labs.

---

## Core Components

| Tool | Purpose |
|---|---|
| **Proxy** | Intercept and modify HTTP/HTTPS traffic |
| **Repeater** | Manually send and modify requests |
| **Intruder** | Automated request manipulation and fuzzing |
| **Scanner** | Automated vulnerability scanning |
| **Decoder** | Encode/decode data |
| **Comparer** | Compare requests and responses |
| **Sequencer** | Analyze token randomness |
| **Logger** | Record HTTP traffic |
| **Target** | Organize and inspect the target application |

Some features are only available in **Burp Suite Professional**.

---

# Proxy

The Proxy intercepts HTTP/HTTPS traffic between the browser and the target.

### Main functions

- Intercept requests
- Modify requests
- Modify responses
- Inspect headers
- Inspect cookies
- View parameters
- Forward or drop requests
- Send requests to other Burp tools

### Interception

| Action | Description |
|---|---|
| **Intercept on** | Stop requests before forwarding |
| **Intercept off** | Forward requests automatically |
| **Forward** | Send intercepted request |
| **Drop** | Discard intercepted request |

---

# HTTP Requests

Basic request structure:

```text
METHOD /path HTTP/1.1
Host: example.com
Header: value

Body
```

### Common HTTP methods

| Method | Purpose |
|---|---|
| `GET` | Retrieve a resource |
| `POST` | Submit data |
| `PUT` | Replace/update a resource |
| `PATCH` | Partially update a resource |
| `DELETE` | Delete a resource |
| `HEAD` | Headers only |
| `OPTIONS` | Supported methods/options |

---

# HTTP Response

Basic response structure:

```text
HTTP/1.1 200 OK
Content-Type: text/html

Response body
```

### Common status codes

| Code | Meaning |
|---|---|
| `200` | OK |
| `201` | Created |
| `204` | No Content |
| `301` | Permanent redirect |
| `302` | Temporary redirect |
| `304` | Not modified |
| `400` | Bad request |
| `401` | Unauthorized |
| `403` | Forbidden |
| `404` | Not found |
| `405` | Method not allowed |
| `429` | Too many requests |
| `500` | Internal server error |
| `502` | Bad gateway |
| `503` | Service unavailable |

---

# Repeater

Repeater is used to manually modify and resend requests.

Useful for:

- Testing parameters
- Modifying headers
- Testing authentication
- Testing access control
- Testing different HTTP methods
- Investigating application behavior
- Comparing responses

Typical workflow:

```text
Proxy → Send to Repeater → Modify → Send → Analyze response
```

---

# Intruder

Intruder automates sending modified requests.

Useful for:

- Fuzzing
- Parameter testing
- Brute-force testing
- Username enumeration
- Password testing
- ID enumeration
- Testing payload variations

### Attack types

| Attack type | Description |
|---|---|
| **Sniper** | One payload position at a time |
| **Battering ram** | Same payload in multiple positions |
| **Pitchfork** | Multiple payload sets in parallel |
| **Cluster bomb** | Combinations of multiple payload sets |

Some Intruder functionality is limited in Burp Community Edition.

---

# Scanner

Burp Scanner performs automated web vulnerability scanning.

Can identify issues such as:

- SQL injection
- Cross-site scripting
- Command injection
- Authentication issues
- Access control issues
- Security misconfigurations
- Information disclosure
- Insecure headers

Scanner is primarily a **Burp Professional** feature.

---

# Target

The Target tab helps organize and inspect the application.

### Site map

Shows discovered:

- Domains
- Directories
- Files
- Parameters
- Requests
- Responses

### Scope

Defines which hosts and URLs are considered in-scope.

Setting scope helps avoid accidentally interacting with unrelated resources.

---

# Decoder

Decoder can encode and decode common data formats.

Useful for:

- URL encoding
- Base64
- Hexadecimal
- HTML encoding
- ASCII
- Hash identification/analysis

Common transformations:

```text
URL encode/decode
Base64 encode/decode
Hex encode/decode
HTML encode/decode
```

---

# Comparer

Comparer compares two pieces of data.

Useful for identifying differences between:

- HTTP responses
- Requests
- Cookies
- Tokens
- Encoded values

Can help determine whether a parameter or request modification changes application behavior.

---

# Sequencer

Sequencer analyzes the quality and randomness of tokens.

Useful for analyzing:

- Session tokens
- CSRF tokens
- Authentication tokens
- Random identifiers

---

# Logger

Logger records HTTP traffic passing through Burp.

Useful for reviewing requests that may have been missed during interception.

---

# Cookies

Cookies are commonly used for:

- Session management
- Authentication
- Preferences
- Tracking

Important attributes:

| Attribute | Purpose |
|---|---|
| `Secure` | Cookie sent only over HTTPS |
| `HttpOnly` | Restricts JavaScript access |
| `SameSite` | Controls cross-site cookie behavior |
| `Domain` | Cookie scope |
| `Path` | URL scope |
| `Expires` | Expiration date |
| `Max-Age` | Lifetime |

---

# Parameters

Common parameter locations:

```text
URL query parameters
POST body
JSON body
HTTP headers
Cookies
Path parameters
```

Things to investigate:

- Hidden parameters
- Unexpected values
- Parameter type changes
- Missing validation
- Duplicate parameters
- Authorization-related parameters
- ID values
- File/path parameters

---

# Encoding

Common encodings encountered during web testing:

| Encoding | Example use |
|---|---|
| URL encoding | HTTP parameters |
| Base64 | Tokens/data |
| Hexadecimal | Binary/data representation |
| HTML encoding | Web content |
| Unicode | Text representation |

Encoding is not encryption. Encoded data can usually be decoded.

---

# HTTPS / TLS

Burp can intercept HTTPS traffic after the Burp CA certificate is trusted by the browser.

Important concepts:

- TLS certificates
- Certificate Authority (CA)
- HTTPS interception
- Burp CA certificate
- TLS versions
- HTTP/1.1
- HTTP/2

---

# Proxy Configuration

Typical setup:

```text
Browser
   ↓
Burp Proxy
   ↓
Target
```

Common proxy listener:

```text
127.0.0.1:8080
```

The browser must be configured to send HTTP/HTTPS traffic through Burp.

---

# Useful Web Testing Areas

When inspecting an application, pay attention to:

### Authentication

- Login
- Registration
- Password reset
- Session handling
- MFA
- Remember-me functionality

### Authorization

- User roles
- Access control
- Object IDs
- Administrative endpoints
- Horizontal privilege escalation
- Vertical privilege escalation

### Input handling

- SQL injection
- XSS
- Command injection
- Path traversal
- File upload
- Template injection

### Session management

- Cookies
- Session IDs
- Token handling
- Session expiration
- Session invalidation

### Business logic

- Price manipulation
- Workflow bypass
- Missing restrictions
- Parameter manipulation
- Race conditions

---

# Useful Burp Concepts

| Concept | Meaning |
|---|---|
| **Request** | Data sent from client to server |
| **Response** | Data returned by server |
| **Proxy** | Intermediary between client and server |
| **Repeater** | Manual request testing |
| **Intruder** | Automated request testing |
| **Scope** | Defined target boundaries |
| **Site map** | Discovered application structure |
| **Payload** | Data inserted into a request |
| **Match** | Response that meets defined conditions |
| **Filter** | Rule used to hide unwanted results |

---

# Common Workflow

```text
1. Configure browser proxy
2. Install Burp CA certificate
3. Define target scope
4. Browse the application
5. Inspect requests and responses
6. Identify interesting parameters
7. Send requests to Repeater
8. Modify and test requests
9. Use Intruder when automation is useful
10. Investigate application behavior
11. Document findings
```

---

# Notes

- Burp is primarily a **web application testing platform**.
- Proxy is used to observe and intercept traffic.
- Repeater is one of the most useful tools for manual testing.
- Intruder is useful for automated payload testing.
- Always inspect both requests **and** responses.
- HTTP status codes alone are not enough. Response body, length, headers, and behavior also matter.
- Scope should be configured carefully when testing real applications.
- Only intercept and test traffic on systems you are authorized to assess.

---

## Resources

- [Burp Suite Documentation](https://portswigger.net/burp/documentation)
- [Web Security Academy](https://portswigger.net/web-security)
