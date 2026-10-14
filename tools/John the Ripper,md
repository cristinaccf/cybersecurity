# John the Ripper

John the Ripper is a password-cracking tool used to recover passwords from hashes and other password-protected data.

Personal notes and reference for using John in cybersecurity labs and CTFs.

---

# Basic Syntax

```bash
john [options] <file>
```

---

# Wordlist Mode

Use a wordlist to test candidate passwords.

```text
--wordlist=<WORDLIST>
```

Common wordlists:

```text
/usr/share/wordlists/
/usr/share/seclists/
```

RockYou is commonly used in CTFs:

```text
rockyou.txt
```

---

# Common Options

| Option | Description |
|---|---|
| `--wordlist=<file>` | Use a wordlist |
| `--format=<format>` | Specify hash format |
| `--show` | Show cracked passwords |
| `--status` | Show current cracking status |
| `--incremental` | Incremental/brute-force mode |
| `--mask=<mask>` | Mask-based cracking |
| `--rules` | Enable wordlist mangling rules |
| `--pot=<file>` | Specify pot file |
| `--session=<name>` | Name a cracking session |
| `--restore=<name>` | Restore a session |
| `--fork=<num>` | Use multiple processes |

---

# Hash Formats

John supports many hash formats.

Specify one with:

```text
--format=<FORMAT>
```

Common formats encountered in labs:

```text
NT
NTLM
NetNTLMv2
md5crypt
bcrypt
sha256crypt
sha512crypt
Raw-MD5
Raw-SHA1
Raw-SHA256
Raw-SHA512
```

List available formats:

```text
--list=formats
```

---

# Hash Identification

Before cracking, determine what type of hash you have.

Useful tools:

```text
hashid
hash-identifier
john
```

John can sometimes identify formats automatically, but specifying `--format` can avoid ambiguity.

---

# Show Cracked Passwords

```text
--show
```

Displays passwords already recovered by John.

Useful after a cracking session.

---

# Wordlist Rules

Rules modify words from a wordlist to generate variations.

```text
--rules
```

Useful for generating variations such as:

```text
password
Password
password1
Password123
```

The exact transformations depend on the selected ruleset.

---

# Incremental Mode

```text
--incremental
```

Attempts passwords using incremental character combinations.

This can become extremely expensive as password length and character set increase.

---

# Mask Mode

```text
--mask=<MASK>
```

Used to define a password pattern.

Useful when part of the password structure is known.

---

# Sessions

### Start a named session

```text
--session=<NAME>
```

### Restore

```text
--restore=<NAME>
```

### Status

```text
--status=<NAME>
```

Useful for long-running cracking jobs.

---

# Pot File

John stores recovered passwords in a pot file.

```text
--pot=<FILE>
```

Already-cracked hashes may therefore be recovered immediately with:

```text
--show
```

---

# Common Workflow

```text
1. Identify the hash type
2. Obtain the hash in a suitable format
3. Select a wordlist or cracking mode
4. Specify the hash format when necessary
5. Start John
6. Monitor progress
7. Show recovered passwords
8. Document the result
```

---

# Useful Commands

| Command | Purpose |
|---|---|
| `john <file>` | Start cracking |
| `john --wordlist=<file> <hashfile>` | Use a wordlist |
| `john --format=<format> <file>` | Specify hash format |
| `john --show <file>` | Show cracked passwords |
| `john --status` | Show status |
| `john --list=formats` | List supported formats |
| `john --rules <file>` | Enable rules |
| `john --incremental <file>` | Incremental mode |
| `john --mask=<mask> <file>` | Mask mode |
| `john --restore=<name>` | Restore session |

---

# Notes

- A hash is not the same thing as an encrypted password.
- The cracking method depends heavily on the hash type.
- Wordlist attacks are usually much faster than unrestricted brute force.
- `--format` is important when John cannot correctly identify the hash.
- `--show` is useful for checking results without running the cracking process again.
- John can work with many formats beyond simple password hashes.
- Only crack credentials or hashes that you are authorized to test.

---

## Resources

- [John the Ripper](https://www.openwall.com/john/)
- [Openwall Documentation](https://www.openwall.com/john/doc/)
