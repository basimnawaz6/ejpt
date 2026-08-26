
## 1. Service Discovery

### Nmap (Start Here)
```bash
# Basic version detection
nmap -sV -p 3306 <target>

# MySQL specific scripts
nmap -p 3306 --script mysql-info,mysql-enum,mysql-databases <target>
```

> [!tip] eJPT Tip
> Always run Nmap first to confirm the service and grab the banner before using Metasploit modules.

---
## 2. Version Detection

### Module: `auxiliary/scanner/mysql/mysql_version`

**Purpose:** Fingerprint the MySQL server version and gather basic information.

**Usage:**
```bash
msfconsole
use auxiliary/scanner/mysql/mysql_version
set RHOSTS <target>
set THREADS 10
run
```

This helps identify outdated MySQL versions that may have known vulnerabilities.

---
## 3. Credential Testing (Brute Force)

### Module: `auxiliary/scanner/mysql/mysql_login`

**Purpose:** Test username and password combinations against MySQL.

**Recommended wordlist:**
```bash
set PASS_FILE /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt
```

**Full usage example:**
```bash
use auxiliary/scanner/mysql/mysql_login
set RHOSTS <target>
set USER_FILE /usr/share/metasploit-framework/data/wordlists/common_users.txt
set PASS_FILE /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt
set THREADS 10
set STOP_ON_SUCCESS true
run
```

> [!note]
> Using `unix_passwords.txt` is smart for Linux-based MySQL installations.

---
## 4. Database Enumeration

### Module: `auxiliary/admin/mysql/mysql_enum`

**Purpose:** Enumerates databases, tables, users, and privileges.

**Usage:**
```bash
use auxiliary/admin/mysql/mysql_enum
set RHOSTS <target>
set USERNAME <valid_username>
set PASSWORD <valid_password>
run
```

---
## 5. Running Custom SQL Queries

### Module: `auxiliary/admin/mysql/mysql_sql`

**Purpose:** Execute arbitrary SQL queries through Metasploit.

**Usage example:**
```bash
use auxiliary/admin/mysql/mysql_sql
set RHOSTS <target>
set USERNAME root
set PASSWORD <password>
set SQL "SHOW DATABASES;"
run
```

---
## 6. File System Enumeration via MySQL

These modules are powerful when the MySQL user has the `FILE` privilege.

### Module: `auxiliary/scanner/mysql/mysql_file_enum
`
```bash
use auxiliary/scanner/mysql/mysql_file_enum
set RHOSTS <target>
set USERNAME <user>
set PASSWORD <pass>
set FILE_LIST /usr/share/metasploit-framework/data/wordlists/directory.txt
run
```

### Module: `auxiliary/scanner/mysql/mysql_writable_dirs
`
```bash
use auxiliary/scanner/mysql/mysql_writable_dirs
set RHOSTS <target>
set USERNAME <user>
set PASSWORD <pass>
set DIR_LIST /usr/share/metasploit-framework/data/wordlists/directory.txt
run
```

> [!warning]
> These modules only work if the MySQL user has the `FILE` privilege.

---
## Bonus: MySQL File Operations (Interesting Extra)

> This goes slightly beyond basic eJPT level but is very relevant in real assessments.

When a MySQL user has the `FILE` privilege, it becomes possible to read files from the server’s filesystem and write files to it. This is a powerful capability that can be abused in post-exploitation.

### What becomes possible:
- Reading sensitive files (e.g. configuration files, `/etc/passwd`, SSH keys)
- Writing files to web directories or cron directories
- In some cases, achieving remote code execution by writing a web shell or a cron job

**Important:** These techniques require the MySQL database account to have the `FILE` privilege, and the target directories must be writable by the MySQL process.

This is why checking for `FILE` privilege and writable directories (using the modules above) is valuable during enumeration.

> [!tip]
> After identifying writable directories, testers sometimes use custom SQL queries to write files. This technique appears in many CTFs and real-world assessments when database access is obtained.

---
## Quick Reference Commands

```bash
# Nmap discovery
nmap -sV -p 3306 --script mysql-info,mysql-enum <target>

# Version scan
use auxiliary/scanner/mysql/mysql_version
set RHOSTS <target>
run

# Login brute force
use auxiliary/scanner/mysql/mysql_login
set RHOSTS <target>
set USER_FILE common_users.txt
set PASS_FILE unix_passwords.txt
set STOP_ON_SUCCESS true
run

# Full enumeration after login
use auxiliary/admin/mysql/mysql_enum
set USERNAME <user>
set PASSWORD <pass>
run

# Run custom SQL
use auxiliary/admin/mysql/mysql_sql
set SQL "SELECT user,host,authentication_string FROM mysql.user;"
run
```

---
## eJPT Exam & Lab Tips

- Start with **Nmap** → then move to Metasploit.
- `mysql_enum` is one of the most valuable modules after getting credentials.
- Always check if the MySQL user has `FILE` privilege — it significantly increases impact.
- Document every valid credential and every database found.
- MySQL access with `FILE` privilege often leads to sensitive data exposure or code execution paths.
