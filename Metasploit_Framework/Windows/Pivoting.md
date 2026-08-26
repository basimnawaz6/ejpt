![[Pasted image 20250913080804.png]]![[Pasted image 20250822124640.png]]
![[Pasted image 20250913082212.png]]
Getting access to a target (pivot) and trying to exploit another target present in the compromised machine's internal network that was not directly accessible from attacker is called pivoting.
 Workflow:
 Hack Victim-1 ---> set autoroute to accessible subnet of victim-1 in meterpreter--->Start hacking victim 2 in the internal network

**Port forwarding:**
![[Pasted image 20250822132751.png]]
First attacker port, then target port and ip. -L means local port.
