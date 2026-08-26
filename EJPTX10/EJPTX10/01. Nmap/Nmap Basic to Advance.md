# 🚀 Recon & Port Scanning
### *Name: Muhammad Salman Shahid*

## 🔍 Fping – Fast Ping Scanner
`fping` is an advanced command-line ping tool used to ping multiple targets quickly.

- `-a`: show alive hosts only
    
- `-g`: generate IP range and scan them
    

---

## 🛰️ Host Discovery Techniques (Nmap)

Host discovery means identifying live hosts on a network before scanning their ports. Nmap uses multiple types of probes for this.

**Basic ICMP Echo Scan:**

```bash
nmap -sn <IP>
```

- Sends echo request to identify online hosts
    
- Works on Linux using ARP on interface like `eth0`
    
- Often blocked by Windows firewalls (ICMP type 8)
    

**Read Nmap Manual:**

```bash
man nmap
```

**Target from a File:**

```bash
nmap -sn -iL targets.txt
```

**TCP SYN Discovery:**

```bash
nmap -PS -sn <IP>
```

- If port is open: responds with SYN-ACK
    
- If closed: responds with RST
    

**TCP ACK Probe (Unreliable):**

```bash
nmap -sn -PA <IP>
```

- If port is open: resets with RST
    
- If closed: no response (unreliable method)
    

---

## 📦 ICMP-Specific Ping Scans

- ICMP Echo Request (default ping):
    
    ```bash
    nmap -sn -PE <IP>
    ```
    
- UDP Ping (uses ICMP unreachable responses):
    
    ```bash
    nmap -sn -PU <IP>
    ```
    
- Alexis Ahmed-style Recon Combo:
    
    ```bash
    nmap -sU -PS21,22,80,443 -PU137,138 -T4 <IP>
    ```
    

---

## 📊 Port Scanning Fundamentals

Port scanning checks whether a host has **open**, **closed**, **filtered**, or **unfiltered** ports.

**Disable Host Discovery:**

```bash
nmap -Pn <IP>
```

- Useful when host discovery is blocked
    
![[Pasted image 20250728202348.png]]

-------------------------------
## 🧰 Tool Highlight: Angry IP Scanner

**Angry IP Scanner** is a powerful GUI tool that:

- Scans IP ranges quickly
    
- Detects live hosts and open ports
    
- Cross-platform and lightweight
    

---

## 🔐 TCP Scan Techniques

### 🔹 Full TCP Connect Scan (`-sT`)

- Uses full 3-way handshake
    
- Doesn't require root privileges
    
- Ends connection with RST
    

```bash
nmap -sT <target>
```

### 🔹 Stealth Scan / SYN Scan (`-sS`)

- Sends SYN, waits for SYN-ACK (open) or RST (closed)
    
- Requires root/admin
    

```bash
nmap -sS <target>
```

### 🔹 Inverse TCP Flags Scan (`-sF`, `-sN`, `-sX`)

- `-sF`: FIN
    
- `-sN`: NULL (no flags)
    
- `-sX`: XMAS (all flags set)
    
- Open ports: No response
    
- Closed ports: RST
    

### 🔹 ACK Flag Probe (`-sA`)

- Sends ACK, checks TTL and Window size
    
- If TTL < 64 or window > 0 → likely open
    

---

## 💥 UDP Scanning

```bash
nmap -sU <target>
```

- No response = possibly open
    
- ICMP Unreachable = closed
    
- Can bypass some IDS, but noisy
    
- Often used by malware/trojans
    

---

## 🛡️ Advanced Scanning Techniques

### 🔸 Verbose & Aggressive Scans

```bash
nmap -vv <target>
nmap -A <target>
```

- `-A`: combines OS detection, version detection, script scanning
    

### 🔸 Scan Specific Ports

```bash
nmap -p 80 <target>        # Scan port 80
nmap -p- <target>          # Scan all 65535 ports
nmap -sV <target>          # Detect service versions
nmap -F <target>           # Fast scan
```

---

## ✂️ Fragmentation & MTU Evasion

**Fragmented Packets (bypass firewalls):**

```bash
nmap -f <target>                   # default fragment
nmap --mtu 16 <target>             # force MTU size to 16
```

- Breaks packets into smaller fragments
    
- Useful to avoid packet inspection
![[Screenshot 2025-07-24 114604.png]]

---

## 👻 Spoofing, Obfuscation & Decoys

- **Decoy IPs:**
    
    ```bash
    nmap -D RND:16 <target>
    ```
    
- **Spoof Source IP:**
    
    ```bash
    nmap -S <spoofed-IP> <target>
    ```
    
- **Idle/Zombie Scan:**
    
    ```bash
    nmap -sI <zombie-IP> <target>
    ```
    
- **Forge Source Port:**
    
    ```bash
    nmap --source-port 53 <target>
    ```
    
- **Spoof MAC Address:**
    
    ```bash
    nmap --spoof-mac 00:11:22:33:44:55 <target>
    ```
    
- **Inject Padding Data:**
    
    ```bash
    nmap --data-length 50 <target>
    ```
    
- **Randomize Hosts:**
    
    ```bash
    nmap --randomize-hosts <target list>
    ```
    
- **Send Corrupted Checksums:**
    
    ```bash
    nmap --badsum <target>
    ```
    

---

## 🧪 SCTP Ping (Rare)

```bash
nmap -sn -PY <IP>
```

---

## 🧱 Custom Packet Crafting Tools

**Colasoft Packet Builder (Windows Only):**

- Used to build custom ARP, TCP, UDP, IP packets
    
- Must run as admin
    

---

## 🪪 Banner Grabbing & OS Detection

### 🔸 Active Banner Grabbing

- Send malformed/special TCP packets and analyze response
    
- Match banners against database
    
- Use tools like:
    
    - `Netcat`
        
    - `Nmap`
        
    - `Telnet`
        

### 🔸 Passive Banner Detection

- Uses sniffing techniques (Wireshark, etc.)
    
- Extracts info like server type, SSL versions, etc.
    
- Doesn’t interact with target
    

---

## 🧵 TCP Connection States

|Status|Description|
|---|---|
|Open|Responds to handshake|
|Closed|Responds with RST|
|Filtered|No response|
|Unfiltered|Accessible but unclear|
|Open|Filtered|

---

## 📈 Windows Scan (Window Size)

```bash
nmap -sW <target>
```

- Sends SYN
    
- Open → SYN-ACK + window size
    
- Closed → RST with different window
    

---

## 🧰 Useful Commands Summary

```bash
nmap -Pn -sS -sV <IP>                  # Stealth + version scan, disable host discovery
nmap -sU -sS -F --host-timeout 5m      # Quick UDP + TCP scan with timeout
nmap -T4 -sS -p 1-1000 <target>        # Stealth scan with timing
nmap -p 22,80,443 -A <target>          # Scan key ports with aggressive scan
```

---

## 🧪 NSE (Nmap Scripting Engine)

Use for:

- Brute-force attacks
    
- Enumeration
    
- Vulnerability scanning
    

Example:

```bash
nmap --script=vuln <target>
```

---

````markdown
⚙️ Timing & Performance Control in Nmap

Nmap timing templates adjust how aggressive or stealthy your scan is.

| Template | Description              |
|----------|--------------------------|
| -T0      | Paranoid (very slow)     |
| -T1      | Sneaky (IDS evasion)     |
| -T2      | Polite (slow, low noise) |
| -T3      | Normal (default)         |
| -T4      | Aggressive (faster)      |
| -T5      | Insane (fastest, risky)  |

Example:
```bash
nmap -T4 -sS <target>
````

---

## 🔄 Host Timeout & Scan Delay

### 🕑 `--host-timeout`

Sets maximum scan time per host.

```bash
nmap --host-timeout 5m <target>
```

Use this to prevent hanging scans on slow/unresponsive hosts.

### 🐢 `--scan-delay`

Introduces delay between probes (good for stealth).

```bash
nmap --scan-delay 2s <target>
```

Can help bypass rate-based firewalls and intrusion detection systems.

---

## 🔓 OS Detection & Version Guessing

### 🎯 Operating System Fingerprinting

```bash
nmap -O <target>
```

- Requires root privileges
    
- Uses TCP/IP stack behavior to guess OS
    
- Might fail behind firewalls or NAT
    

### 🎲 Version Guessing for Unclear Results

```bash
nmap -sV --version-all <target>
nmap -sV --version-trace <target>
nmap -sV --version-intensity 9
nmap -sV --version-light
```

### 👀 Disable DNS Resolution

```bash
nmap -n <target>
```

Saves time by skipping DNS lookups.

---

## 📄 Output Formats & Report Saving

**Save in all formats at once:**

```bash
nmap -oA output <target>
```

This gives you:

- `output.nmap` → Normal output
    
- `output.gnmap` → Grepable format
    
- `output.xml` → Machine-readable XML
    

**Individual formats:**

```bash
nmap -oX result.xml <target>
nmap -oG result.gnmap <target>
nmap -oN result.txt <target>
```

### 💡 Convert XML to HTML Report

Using `xsltproc`:

```bash
xsltproc result.xml -o result.html
```

---

## 📦 Nmap Scripting Engine (NSE)

Powerful feature that uses Lua scripts to:

- Enumerate services
    
- Brute-force passwords
    
- Scan for known vulnerabilities
    

### 🔹 Scan with Default Scripts

```bash
nmap -sC <target>
```

### 🔹 Run Specific Scripts

```bash
nmap --script=http-title <target>
```

### 🔹 Vulnerability Detection

```bash
nmap --script=vuln <target>
```

### 🔹 Script Categories:

- `auth`, `brute`, `vuln`, `safe`, `exploit`, `dos`, `intrusive`, etc.
![[Pasted image 20250728215114.png]]
    

### 🔹 Find Scripts

```bash
ls /usr/share/nmap/scripts/
```

---

## 🌐 Packet Tracing

### 🔬 Trace All Packets During Scan

```bash
nmap --packet-trace <target>
```

Useful for debugging or studying how Nmap builds packets.

---

## 🧱 Fragmentation and MTU Evasion

### 🔹 What Fragmentation Does:

Breaks Nmap packets into smaller chunks to:

- Bypass deep packet inspection (DPI)
    
- Bypass some IDS/IPS
    
- Confuse firewalls looking for full headers
    

### 🔹 Basic Fragmentation

```bash
nmap -f <target>
```

Sends tiny fragments (8 bytes each).

### 🔹 Set Custom MTU Size

```bash
nmap --mtu 24 <target>
```

Forces packet size to 24 bytes. MTU must be divisible by 8.

**Best practice:** Use uncommon MTU values (e.g. 24, 88) to confuse firewalls.

---

## 🔍 Disable ARP Ping (for stealth on local networks)

```bash
nmap -sn -disable-arp-ping <target>
```

---

## 🧨 Hping3 – Custom Packet Crafting

`hping3` allows crafting raw TCP/IP packets for:

- Firewall testing
    
- OS fingerprinting
    
- Port scanning
    
- DoS simulation
    

### 🔸 SYN Scan

```bash
hping3 -S <target> -p 80 -c 1
```

### 🔸 ACK Scan (firewall evasion)

```bash
hping3 -A <target> -p 80 -c 1
```

### 🔸 FIN Scan

```bash
hping3 -F <target> -p 80 -c 1
```

### 🔸 Ping with Spoofed IP

```bash
hping3 -1 -a 192.168.1.100 <target>
```

---

## 🧠 TCP Idle/Zombie Scan (Why It’s Famous)

```bash
nmap -sI <zombie-ip> <target>
```

**How it works:**

- Sends spoofed packets from an idle third-party host (zombie)
    
- Uses predictable IP ID fields to infer port states
    
- No packets come directly from your IP → stealth AF
    

**When Target Port is Open:**

- Zombie’s IP ID changes by +2 → means scan triggered a response
    

**When Target Port is Closed:**

- IP ID changes by +1 → no response from target
    

**Why it's loved:**

- **Completely stealthy**
    
- **Bypasses most firewalls and logging**
    
- **Used in real-world red team ops**
    


---
## 🧨 TCP Maimon Scan (`-sM`)

> A legacy TCP scan method using FIN/ACK to exploit BSD behavior. Named after its discoverer, **Uriel Maimon**.

---

### 📖 Origin & History

- 📜 **Discovered by**: Uriel Maimon in **Phrack Magazine Issue #49 (Nov 1996)**.
- 🛠 **First added to Nmap**: Two Phrack issues later.
- 🧬 **Same goal as**: NULL (`-sN`), FIN (`-sF`), and Xmas (`-sX`) scans — stealth TCP probing.
- 📘 **RFC 793** says: Any unexpected FIN/ACK should be answered with **RST**, whether port is **open or closed**.
- 😈 **But**: Many **BSD-derived systems** silently drop these packets if the port is **open** — creating a fingerprinting opportunity.

---

### 🧬 How it Works

- Sends **TCP FIN/ACK** probe.
- **Expected behavior** (RFC 793): Target sends **RST**.
- **Observed BSD bug**: If port is open, packet is **silently dropped**.
- This lets Nmap infer port states **even without full TCP handshake**.

---

### 📊 Response Interpretation

| Probe Response | Interpreted As    |
|----------------|-------------------|
| **No response (dropped)** | 🟢 `open|filtered` |
| **TCP RST**               | 🔴 `closed`        |
| **ICMP unreachable** (type 3, code 1,2,3,9,10,13) | 🟡 `filtered` |

---
## 🧠 Final Notes

- Understand TCP/IP behavior deeply to interpret scan results correctly
    
- Firewalls, NAT, IDS can skew your results — combine active and passive recon
    
- Always verify with Wireshark or packet captures if unsure
    

---

## 🛠 Packet Capture with Wireshark

**Steps:**

1. Start Wireshark
    
2. Filter by target IP:
    
    ```
    host <target IP>
    ```
    
3. Start scanning (e.g., `nmap -sS`)
    
4. Look for SYN, ACK, RST flags in captured packets
    

**For deeper visibility**, use:

```bash
tcpdump -i eth0 host <target> -w capture.pcap
```

---

### 🎯 Quote to Remember

> **"Knowing your enemy is winning half the war."**

---
