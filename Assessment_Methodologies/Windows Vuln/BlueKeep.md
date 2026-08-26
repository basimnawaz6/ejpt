### **BlueKeep Vulnerability (CVE-2019-0708)**

- **What it is:** A Windows Remote Desktop Protocol (RDP) vulnerability.
- **The issue:** Windows RDP service had a flaw in handling certain requests during the connection setup.
- **Effect:** An attacker could connect via RDP and run code on the target computer **without a password** (Remote Code Execution).
- **Impact:** Could spread like a worm, but mostly used for targeted attacks.
- **Target**: Windows Remote Desktop Services (RDP)
- **Affected Systems**: Windows 7, Server 2008/R2, XP
- **Type**: **Pre-auth RCE (Remote Code Execution)**
- **Wormable**: Yes (can self-propagate like WannaCry)
- **Exploitation**: Allows attacker to run code **without login**
- **Patched by Microsoft**: Yes, in May 2019
