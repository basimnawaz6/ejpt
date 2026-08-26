
# 🧠 Enumeration Master Note – Deep Recon Phase

> **Definition**: Enumeration is the **active process of connecting to target services** to extract detailed, structured information — users, groups, shares, banners, configurations, and misconfigurations — **post-scanning**, using focused tools and techniques.

---

## 🎯 Goals of Enumeration

- 🔍 Discover users, groups, and computers
    
- 🗂 List network shares and exposed files
    
- 🌐 Reveal internal DNS or LDAP structures
    
- 📦 Interact with services (FTP, HTTP, MySQL, etc.) to extract banners and behaviors
    
- 🔐 Identify misconfigs for privilege escalation or lateral movement
    

---

## 📌 Commonly Enumerated Ports & Protocols

|Protocol|Port(s)|Service|
|---|---|---|
|DNS|UDP/TCP 53|Zone transfers, records|
|SMB|TCP 139/445|Shares, users, groups|
|NetBIOS|UDP 137/138|Computer names, sessions|
|LDAP|TCP/UDP 389|Active Directory data|
|HTTP|TCP 80/443|Web pages, admin panels|
|FTP|TCP 21|File sharing|
|SNMP|UDP 161/162|Network device information|
|SMTP|TCP 25|Email user validation|
|NFS|TCP/UDP 2049|Network file shares (Linux)|
|MySQL|TCP 3306|Database user/data access|

---

## 🗂️ Service-by-Service Enumeration

---

### 📂 SMB (Server Message Block)

> SMB is a Windows-based file sharing protocol. Enumerating it can leak file shares, users, and permissions.

- **Ports**: TCP 445, TCP 139
    
- **What to look for**: Shared folders, user/group info, service banners
    
- **Tools**:
    
    - `enum4linux -a <IP>`
        
    - `smbclient -L //<IP> -N`
        
    - `smbmap -H <IP>`
        
    - `rpcclient -U "" <IP>`
        
    - `nmap -p 139,445 --script=smb*`
        


---

### 📚 LDAP (Lightweight Directory Access Protocol)

> LDAP is used in enterprise networks (like Active Directory) to store user, group, and computer data.

- **Port**: TCP 389
    
- **What to look for**: Users, OUs, groups, computers
    
- **Tools**:
    
    - `ldapsearch -x -h <IP> -b "dc=example,dc=com"`
        
    - `nmap -p 389 --script=ldap*`
        
    - `enum4linux`, `CME` (CrackMapExec)
`
        

---

### 🌐 DNS (Domain Name System)

> DNS resolves domain names to IPs. Enumeration may expose subdomains, internal hosts, and network structure.

- **Ports**: UDP/TCP 53
    
- **What to look for**: Zone transfers, subdomains, misconfigs
    
- **Tools**:
    
    - `dig axfr @<NS> domain.com`
        
    - `dnsrecon`, `dnsenum`
        
    - `nslookup` / `host`
        


---

### 🧱 HTTP/HTTPS

> HTTP(S) enumeration reveals site structure, hidden pages, technologies, and potential vulnerabilities.

- **Ports**: TCP 80 / 443
    
- **What to look for**: Login portals, admin pages, tech stacks
    
- **Tools**:
    
    - `whatweb`, `nikto`, `gobuster`, `dirb`, `ffuf`
        
    - `curl -I http://<target>` (headers)
        


---

### 📡 SNMP (Simple Network Management Protocol)

> SNMP is used to manage network devices. Misconfigurations expose internal data.

- **Ports**: UDP 161 (queries), UDP 162 (traps)
    
- **What to look for**: Interfaces, routing tables, system info
    
- **Tools**:
    
    - `snmpwalk -v1 -c public <IP>`
        
    - `snmp-check`, `onesixtyone`
        


---

### 📨 SMTP (Simple Mail Transfer Protocol)

> SMTP can be abused to enumerate valid usernames using legacy commands like `VRFY`.

- **Port**: TCP 25
    
- **What to look for**: Valid usernames
    
- **Tools**:
    
    - `telnet <IP> 25` → try `VRFY`, `EXPN`
        
    - `nmap -p 25 --script=smtp-enum-users`
        


---

### 💾 NFS (Network File System)

> NFS allows Linux/Unix machines to share files. Enumeration reveals mountable remote file systems.

- **Port**: TCP/UDP 2049
    
- **What to look for**: Exported directories
    
- **Tools**:
    
    - `showmount -e <IP>`
        
    - `mount -t nfs <IP>:/share /mnt/share`
        
    - `nmap -p 2049 --script=nfs*`
        

---

### 🛠 FTP (File Transfer Protocol)

> FTP is used for file sharing. Weak configurations allow anonymous logins.

- **Port**: TCP 21
    
- **What to look for**: Anonymous access, readable files
    
- **Tools**:
    
    - `ftp <IP>`
        
    - `nmap -p 21 --script=ftp*`
        

---

### 🧳 NetBIOS

> NetBIOS is used on LANs to share name and session info between Windows machines.

- **Ports**: UDP 137 (Name), UDP 138 (Datagram), TCP 139 (Session)
    
- **What to look for**: Hostnames, sessions, shares
    
- **Tools**:
    
    - `nbtscan <IP>`
        
    - `nmap -p 137 --script nbstat`
        
    - `enum4linux`
        

---

### 🧬 MySQL

> MySQL is a popular database. Enumeration checks for weak creds and access to sensitive data.

- **Port**: TCP 3306
    
- **What to look for**: Default logins, accessible databases
    
- **Tools**:
    
    - `mysql -u root -h <IP> -p`
        
    - `nmap -p 3306 --script=mysql*`

---

## 🧨 Advanced Enumeration Techniques

- 🧠 **Banner Grabbing**: `nc <IP> <port>`, `curl`, or `telnet`
    
- 🔁 **Chaining with proxychains/VPNs**: for internal/pivoted enum
    
- 🧠 **Service Fuzzing**: `ffuf`, `wfuzz`, or Burp Intruder
    
- 🧠 **Authenticated Enumeration**: Use valid credentials or sessions to go deeper (CME, WinRM, SMB auth)
    
- 📌 **Metasploit Workspace**: `workspace -a target1` to manage enum cleanly
    
- 📦 **Post-exploit Recon**: `meterpreter` shell → background → modules
    

---

## 🛡️ Defensive Tips (Countermeasures)

- ❌ Disable SMBv1 and NetBIOS
    
- 🔐 Restrict LDAP and RPC to trusted systems
    
- 🚫 Block anonymous FTP and SNMP community "public"
    
- 🧱 Configure DNS to prevent zone transfers
    
- 🔄 Use internal firewalls & segmented VLANs
    

---

## ✅ Pro Enumeration Habits

- 🕵️‍♂️ Start wide → go deep on each service
    
- 🧪 Confirm ports with multiple tools
    
- 🧾 Keep structured logs/output (e.g., in Obsidian or Markdown)
    
- 🔍 Screenshot and note versions for exploits later
    
- 🔁 Repeat enum **after gaining access** — new info appears
    

---

