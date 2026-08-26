- **What it is:** A Windows SMBv1 (file sharing protocol) vulnerability.
- **The issue:** Windows didn’t properly handle certain specially crafted SMB packets.
- **Effect:** An attacker could send those packets to a vulnerable computer over the network and run their own code **without logging in** (Remote Code Execution).
- **Impact:** Used by WannaCry ransomware to spread automatically between computers.

- **CVE ID**: **CVE-2017-0144**
- **Discovered by**: NSA (leaked by Shadow Brokers in 2017)
- **Exploits**: **Microsoft SMBv1 (Server Message Block version 1)** protocol
- **Vulnerability Type**: **Remote Code Execution (RCE)**
- **Attack Mechanism**:
   - Sends specially crafted packets to vulnerable SMBv1 service.
   - Allows attacker to **execute arbitrary code remotely without authentication**.
- **Affected Systems**:
- Windows XP
- Windows Vista
- Windows 7
- Windows 8
- Windows 10 (older versions)
- Windows Server 2003, 2008, 2012, etc.

- **Used in Real-World Attacks**:
- **WannaCry** ransomware (May 2017)
- **NotPetya**, **Retefe**, and other malware

- **Patch Released**: **March 2017** (MS17-010)

- **Detection & Prevention**:
- Disable SMBv1
- Apply MS17-010 patch
- Use network-level firewalls to block SMB ports (typically TCP 445)
- Monitor for unusual SMB traffic
