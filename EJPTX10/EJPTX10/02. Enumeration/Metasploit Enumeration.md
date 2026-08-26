## 📦 Metasploit Auxiliary Modules for Enumeration

### 🔐 SMB Enumeration

```bash
search type:auxiliary smb
```

**Key Modules:**

- `auxiliary/scanner/smb/smb_version` — Identify SMB version running on host
    
- `auxiliary/scanner/smb/smb_enumusers` — Enumerate valid users via SMB
    
- `auxiliary/scanner/smb/smb_enumshares` — List all accessible shares
    
- `auxiliary/scanner/smb/smb_login` — Brute-force SMB logins
    
- `auxiliary/scanner/smb/smb_lookupsid` — Enumerate SIDs and usernames
    

---

### 📇 LDAP Enumeration

```bash
search type:auxiliary ldap
```

**Key Modules:**

- `auxiliary/gather/ldap_query` — Perform arbitrary LDAP queries
    
- `auxiliary/scanner/ldap/ldap_login` — LDAP login brute force
    
- `auxiliary/admin/ldap/ldap_add` — Inject LDAP entries (if writable access exists)
    

---

### 🖥️ SNMP Enumeration

```bash
search type:auxiliary snmp
```

**Key Modules:**

- `auxiliary/scanner/snmp/snmp_enum` — Extract SNMP system info
    
- `auxiliary/scanner/snmp/snmp_enumusers` — Enumerate user accounts
    
- `auxiliary/scanner/snmp/snmp_login` — Brute force community strings
    
- `auxiliary/scanner/snmp/snmp_enumshares` — Check for shared folders
    

---

### 🛢️ MySQL Enumeration

```bash
search type:auxiliary mysql
```

**Key Modules:**

- `auxiliary/scanner/mysql/mysql_version` — Detect MySQL version
    
- `auxiliary/scanner/mysql/mysql_login` — Brute-force credentials
    
- `auxiliary/admin/mysql/mysql_sql` — Run arbitrary SQL (if access gained)
    
- `auxiliary/admin/mysql/mysql_enum` — Enumerate databases, tables, users
    

---

### 📂 NFS Enumeration (Network File System)

```bash
search type:auxiliary nfs
```

**Key Modules:**

- `auxiliary/scanner/nfs/nfs_mount` — List mountable shares
    
- `auxiliary/scanner/nfs/nfsmount` — Identify accessible shares and permissions
    
- `auxiliary/admin/nfs/nfs_export` — Exploit misconfigured NFS exports
    

---

### 🌐 FTP Enumeration

```bash
search type:auxiliary ftp
```

**Key Modules:**

- `auxiliary/scanner/ftp/ftp_login` — Brute-force FTP credentials
    
- `auxiliary/scanner/ftp/ftp_version` — Detect FTP server software/version
    
- `auxiliary/scanner/ftp/anonymous` — Check for anonymous access
    
- `auxiliary/admin/ftp/ftp_put` — Upload file (if write permission)
    
- `auxiliary/scanner/ftp/ftp_bounce` — Perform FTP bounce scan (old technique)
    

---

### 🌍 HTTP Enumeration & Directory Bruteforce

```bash
search type:auxiliary http
```

**Key Modules:**

- `auxiliary/scanner/http/apache_userdir_enum` — Bruteforce Apache UserDir directories
    
- `auxiliary/scanner/http/brute_dirs` — Bruteforce common web directories
    
- `auxiliary/scanner/http/dir_scanner` — Identify valid web directories
    
- `auxiliary/scanner/http/dir_listing` — Detect enabled directory listings
    
- `auxiliary/scanner/http/files_dir` — Look for interesting downloadable files
    
- `auxiliary/scanner/http/http_login` — HTTP basic/digest authentication brute force
    
- `auxiliary/scanner/http/http_header` — Pull server response headers
    
- `auxiliary/scanner/http/http_version` — Detect HTTP version and banner
    
- `auxiliary/scanner/http/http_put` — Test for PUT method file upload capability
    
- `auxiliary/scanner/http/robots_txt` — Enumerate disallowed paths from robots.txt
    

---

### 🔑 SSH Enumeration

```bash
search type:auxiliary ssh
```

**Key Modules:**

- `auxiliary/scanner/ssh/ssh_version` — Identify SSH server version
    
- `auxiliary/scanner/ssh/ssh_login` — Brute-force SSH credentials
    

**Useful Wordlists:**

- `/usr/share/metasploit-framework/data/wordlists/common_users.txt`
    
- `/usr/share/metasploit-framework/data/wordlists/common_passwords.txt`
    

---

## ✅ Pro Tip for All Modules

In `msfconsole`, after selecting any module:

```bash
use auxiliary/scanner/ftp/ftp_login
show options
set RHOSTS <target>
run
```

---

