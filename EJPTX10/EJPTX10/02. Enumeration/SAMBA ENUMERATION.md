
## 1. Service Discovery with Nmap

```bash
# Scan both TCP and UDP ports
nmap -sU -sT -p 137,138,139,445 <target>

# Recommended scan with scripts
nmap -p 139,445 --script smb-os-discovery,smb-security-mode,smb-enum-shares,smb-enum-users,smb-vuln-ms17-010 <target>
```

**Useful Nmap SMB Scripts:**
| Script                        | Purpose                                      |
|-------------------------------|----------------------------------------------|
| `smb-os-discovery`            | Detects OS, workgroup, and SMB version       |
| `smb-security-mode`           | Shows signing requirements and SMBv1 status  |
| `smb-enum-shares`             | Lists shares (including hidden ones)         |
| `smb-enum-users`              | Enumerates users via SMB                     |
| `smb-vuln-ms17-010`           | Checks for EternalBlue vulnerability         |

---

## 2. NetBIOS Enumeration

### Tool: `nmblookup`

```bash
nmblookup -A demo.ine.local
```

**What it does:**
- Queries the NetBIOS name table
- Reveals computer name, workgroup/domain, and MAC address
- Helps identify the role of the machine (workstation, domain controller, etc.)

---

## 3. Share Enumeration

### Tool: `smbclient`

```bash
# List shares anonymously (null session)
smbclient -L demo.ine.local -N

# Connect to a specific share
smbclient //demo.ine.local/ShareName -N
```

**Useful flags:**
- `-N` → No password (null session)
- `-U username%password` → Authenticated access
- `-L` → List shares

---

## 4. RPC Enumeration

### Tool: `rpcclient`

```bash
# Null session RPC enumeration
rpcclient -U "" -N demo.ine.local
```

**Common commands inside rpcclient:**
```bash
enumdomusers          # Enumerate domain users
enumdomgroups         # Enumerate domain groups
queryuser <username>  # Get details about a specific user
srvinfo               # Server information
netshareenum          # List shares via RPC
```

> [!note]
> `rpcclient` is very powerful for enumerating users and groups even without credentials in some misconfigured environments.

---

## 5. Metasploit SMB Modules

### Version Detection
```bash
use auxiliary/scanner/smb/smb_version
set RHOSTS demo.ine.local
run
```

### Share Enumeration
```bash
use auxiliary/scanner/smb/smb_enumshares
set RHOSTS demo.ine.local
set SMBUser <username>          # or leave blank for null session
set SMBPass <password>
run
```

### User Enumeration
```bash
use auxiliary/scanner/smb/smb_enumusers
set RHOSTS demo.ine.local
run
```

### SMB Login / Brute Force
```bash
use auxiliary/scanner/smb/smb_login
set RHOSTS demo.ine.local
set USER_FILE /usr/share/metasploit-framework/data/wordlists/common_users.txt
set PASS_FILE /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt
set THREADS 10
set STOP_ON_SUCCESS true
run
```

---

## 6. Other Useful Tools

| Tool            | Command Example                              | Best For                     |
|-----------------|----------------------------------------------|------------------------------|
| **enum4linux**  | `enum4linux -a demo.ine.local`               | All-in-one SMB enumeration   |
| **smbmap**      | `smbmap -H demo.ine.local -u "" -p ""`       | Share permission mapping     |
| **crackmapexec**| `crackmapexec smb demo.ine.local -u '' -p ''` | Modern enumeration & attacks |

> [!tip] eJPT Recommendation
> Start with `enum4linux -a` — it combines many of the above techniques into one command and gives excellent output.

---

## Common Findings & What They Mean

| Finding                        | Risk Level | Possible Next Step                     |
|--------------------------------|------------|----------------------------------------|
| Null session allowed           | Medium     | Enumerate users, shares, groups        |
| Anonymous share access         | High       | Read/write sensitive files             |
| SMBv1 enabled                  | High       | Check for MS17-010 (EternalBlue)       |
| Signing not required           | Medium     | Relay attacks possible (advanced)      |
| Weak/default credentials       | High       | Login and move to post-exploitation    |
| Admin shares (C$, ADMIN$)      | Very High  | Direct system access if credentials found |

---

## Quick Reference Commands

```bash
# Full Nmap SMB scan
nmap -p 139,445 --script smb-os-discovery,smb-enum-shares,smb-enum-users <target>

# NetBIOS lookup
nmblookup -A <target>

# List shares (null session)
smbclient -L <target> -N

# RPC enumeration
rpcclient -U "" -N <target>

# All-in-one tool (recommended)
enum4linux -a <target>

# Metasploit share enumeration
use auxiliary/scanner/smb/smb_enumshares
set RHOSTS <target>
run
```

---

## eJPT Exam & Lab Tips

- Always start with **Nmap** scanning both TCP 445 and UDP 139.
- Use `enum4linux -a` early — it saves a lot of time.
- Null sessions (`-N` or empty username/password) are still common in labs.
- Document every share you find and whether it allows anonymous access.
- If you find writable shares, check if you can upload files (potential for privilege escalation or web shell).
- SMB is often the easiest way to enumerate users on Windows/Samba targets.

---

