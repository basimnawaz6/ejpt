1. When a privileged user tries to scan targets on a local network (Ethernet), Nmap uses ARP requests. A privileged user is `root` or a user who belongs to `sudoers` and can run `sudo`.
2. When a privileged user tries to scan targets outside the local network, Nmap uses ICMP echo requests, TCP ACK (Acknowledge) to port 80, TCP SYN (Synchronise) to port 443, and ICMP timestamp requests.
3. When an unprivileged user tries to scan targets outside the local network, Nmap resorts to a TCP 3-way handshake by sending SYN packets to ports 80 and 443.

For ARP SCAN :
we use the Nmap -PR -sn <target>

FOr ICMP Scan 
To use ICMP echo requests to discover live hosts, add the option `-PE` option. (Remember to add `-sn` if you don’t want to follow that with a port scan.)

**ICMP Type 17**

Similarly, Nmap uses address mask queries (ICMP Type 17) and checks whether it gets an address mask reply (ICMP Type 18). This scan can be enabled with the option `-PM`. As shown in the figure below, live hosts are expected to reply to ICMP address mask requests.


**ICMP Timestamp**

Because ICMP echo requests tend to be blocked, you might also consider ICMP Timestamp or ICMP Address Mask requests to tell if a system is online. Nmap uses a timestamp request (ICMP Type 13) and checks whether it will get a Timestamp reply (ICMP Type 14). Adding the `-PP` option tells Nmap to use ICMP timestamp requests. As shown in the figure below, you expect live hosts to reply.



TCP SCAN:
TCP SYN PING
nmap -PS -sn <target>
if you are are non preovelige user its send it with the proper 3 way handshake but if you are prebelige user its only send the syn packt

If you want Nmap to use TCP SYN ping, you can do so via the option `-PS` followed by the port number, range, list, or a combination of them. For example, `-PS21` will target port 21, while `-PS21-25` will target ports 21, 22, 23, 24, and 25. Finally, `-PS80,443,8080` will target the three ports 80, 443, and 8080.



TCP ACK ATTACK
only occure with root proveliges
nmap -PA -sn <target>


UDP Ping attack 

nmap -PU -sn <target>


Rverse DNS lookup using namp


nmap -R ( for reverse dns lookup)

nmap -n (disblae the lookup

![[Pasted image 20260709113512.png]]






PORT SCANNING


![[Pasted image 20260709114838.png]]





TCP SYN PORT SCAN

nmap -sT -Pn <target>


TCP ONLY SYN ATTACK ( ROOT NEEDED)


nmap -sS -Pn <target>




SNEAKY TASK

You can control the scan timing using `-T<0-5>`. `-T0` is the slowest (paranoid), while `-T5` is the fastest. According to the Nmap manual page, there are six templates:

- paranoid (0)
- sneaky (1)
- polite (2)
- normal (3)
- aggressive (4)
- insane (5)
  
  
  
  ![[Pasted image 20260709122441.png]]
  
  
  
  NULL SCAN 
  
  ![[Pasted image 20260709123529.png]]
  
  
  
  ![[Pasted image 20260709123537.png]]
  
  
  sudo nmap -sN 10.48.170.112
  
  
  
FIN SCAN

ONly set the FIN FLAG TO 1

![[Pasted image 20260709123930.png]]



![[Pasted image 20260709123941.png]]



udo nmap -sF 10.48.170.112



XMAS SCAN 

SET THE FIN URG AND PUSH FLAG TO 1

![[Pasted image 20260709124035.png]]


![[Pasted image 20260709124043.png]]


sudo nmap -sX 10.48.170.112


MAIMON SCAN

In this scan some system using the old bsd when send a fin and ACK pakcet sent they are sent back a alformed packer whule closed prot just tell the port is closed with RST packer


Window Scan

Another similar scan is the TCP window scan. The TCP window scan is almost identical to the ACK scan; however, it examines the TCP Window field of the RST packets returned. On specific systems, this can reveal that the port is open. You can select this scan type with the option `-sW`. As shown in the figure below, we expect to get an RST packet in reply to our “uninvited” ACK packets, regardless of whether the port is open or closed.


sudo nmap -sW 10.48.170.112



CUstom scan



If you want to experiment with a new TCP flag combination beyond the built-in TCP scan types, you can do so using `--scanflags`. For instance, if you want to set SYN, RST, and FIN simultaneously, you can do so using `--scanflags RSTSYNFIN`. As shown in the figure below, if you develop your own custom scan, you need to understand how the different ports will behave to correctly interpret the results in different scenarios



DECOY SCAN IN NMAP

You can launch a decoy scan by specifying a specific or random IP address after `-D`. For example, `nmap -D 10.10.0.1,10.10.0.2,ME 10.48.170.112` will make the scan of 10.48.170.112 appear as coming from the IP addresses 10.10.0.1, 10.10.0.2, and then `ME` to indicate that your IP address should appear in the third order. Another example command would be `nmap -D 10.10.0.1,10.10.0.2,RND,RND,ME 10.48.170.112`, where the third and fourth source IP addresses are assigned randomly, while the fifth source is going to be the attacker’s IP address. In other words, each time you execute the latter command, you would expect two new random IP addresses to be the third and fourth decoy sources.





rREAspmn
sudo nmap -sS --reason 10.48.170.112


![[Pasted image 20260709140939.png]]


![[Pasted image 20260709140956.png]]




SERVICE VERSION DETECTION

Adding `-sV` to your Nmap command will collect and determine service and version information for the open ports. You can control the intensity with `--version-intensity` LEVEL where the level ranges from 0(the lightest) to 9(the most complete). `-sV --version-light` has an intensity of 2, while `-sV --version-all` has an intensity of 9.

It is important to note that using `-sV` will force Nmap to proceed with the TCP 3-way handshake and establish the connection. The connection establishment is necessary because Nmap cannot discover the version without establishing a connection fully and communicating with the listening service. In other words, a stealth SYN scan `-sS` is not possible when the -`sV` option is chosen.







  
  
  
  nmap scripts
  
LS * htpp

![[Pasted image 20260709212314.png]]


