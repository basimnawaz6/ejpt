![[Pasted image 20250822064513.png]]

To enable RDP at a target system, refer to the screenshot below:
![[Pasted image 20250822065536.png]]

To change admin password on Windows
`net user Administrator hacker123_321`
This requires highest privs and not recommended as its easily detectable
 Logging into rdp:
 
 **On linux:**
`xfreerdp /u:administrator /p:hacker123_321 /v:<target_ip>`

