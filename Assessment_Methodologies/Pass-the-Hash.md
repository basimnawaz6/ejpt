- Exploitation technique involving capturing hashes/passwords and using them to authenticate target legitimately via smb.
- Admin hash required for lateral movement if same on each machine.
**Tools Used:**
- Mimikatz: Steals Windows credentials (passwords, hashes, tickets) from memory.
- kiwi: Metasploit module version of Mimikatz for stealing credentials.
- PsExec: Executes commands on remote Windows systems using SMB.
- **Impacket** (Python): Collection of Python scripts for network protocol exploitation and post‑exploitation (SMB, RDP, etc.).

- CrackMapExec (CME): Swiss‑army knife for attacking and managing large Windows/Active Directory networks. 
![[Pasted image 20250726053808.png]]
- winexe: Runs commands on remote Windows machines from Linux using SMB.
- smbclient (Samba): Command‑line tool to access and transfer files over SMB shares.
- PowerSploit’s Invoke‑PTH: PowerShell tool to perform **Pass‑the‑Hash** attacks for authentication without knowing the plaintext password.

