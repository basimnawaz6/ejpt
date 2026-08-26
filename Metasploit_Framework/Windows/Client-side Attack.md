![[Pasted image 20250813131755.png]]

msfvenom
![[Pasted image 20250813155557.png]]

**For generating Windows payloads**
![[Pasted image 20250813162014.png]]
**-a**-> target architecture
**-p** -> payload
set host/port where connection will be established (your kali)
**-f**-> format of the file (like exe)  
**'>'** -> location where to save payload file (look at the name mentioned on the command)
Make sure to use relevant extension

For available executable formats and encoding transformations:
`msfvenom --list formats`

**For generating Linux payloads**
![[Pasted image 20250816053808.png]]

**For encoding payload**
![[Pasted image 20250816062345.png]]

Iterations can be added, e.g add 10 before mentioning encoding format it will go through 10 times. More iteration=higher chance to evade AV

**Metasploit Resource Script**
![[Pasted image 20250816110731.png]]
