Fping is a command tool that is used ti advanced ping scan 
fping targer name
fping -a -g 10.10.23.89 
Host dicovery techniques:
its is a tecniques in ehihc we use nmap to find out which hosts are open using echo reuqests 
nmap -sn <ip>
we use man nmap to open all the manual of the nmap
nmap sent arp requests to eth0
sn is used to only host scan restricrted the port scan and make sure its donot work on winows becuase windows oftens block icmp echo requests type 8
if we want to give a list of targets
nmap -sn -iL <IP>
nmap -PS -sn <ip> if its open it wellrespond wiht tcp sin ack and then tcp rst if the port is close.
nmap -sn -PA <IP> its not arealible tecbnuques and if the port is open its reapsnd with reset packert but when port is closed not respond
Icmp specific ping scan:
nmap -sn -PE <IP>
its is icmp echo request packet to check to check the host discovery...
nmap -sn -PU <IP> its a udp host discovery scanning 
nmap -su -PS 21,22,80,443 -PU137,138 -T4 <IP> its alexis ahmed ejpt master approch
![[Screenshot 2025-07-23 115926.png]]

Port Scanning:
its a technique in ehihc we scan all the open filetered closed or unfltered peorts on a host....
![[Pasted image 20250728202348.png]]

nmap -Pn (its deable the host dicovery scan) 
tcp full connection three way handshake when you are not a root user and if you are a root root sysn packet sents

                  "Knowing your enemy is winning half the war"

Tool:
ANgry ip scanner is a tool that is used to scan all the avaibale live host a powefull (gpt make it in little bit good way)

TCP connect / Full Open scan (-sT):
. using a three way handshake
.tears connection by sending rst
. no root permission rewqueered
. when sevrer sent RST (closed)

Stealth (half-open scan)(-sS):
.connection half open scan
.sent syn if open (syn + ACK)
.closed (RST)

TCP inverse flag (-sF,-sN)(its giave sfalse posibetive also):
. client sent null or any flag jo set ho
. if no reply port open if reply with ack/rst then port closed.

XMAS Scan: (-sX)(false poosibtive):
.send all flags set 
.sent apcket if open  no response
.sent packet but receiev rst/act if closed\

ACK flag probe scanning -sA 
.Attacket send tcp probece with ack then anayzyle header window size 
if TTL less then 64 port is open 
window sicz non zero port open 

ICMP uneacbel 
port filtered
 attacker ssends ack wiht random sequence no respnsxe not come menas port is filter 


UDP SCAN:
.no respnse  no firewall port is open
..respnse   icmp  packet unreacbale  closed
.spyware,trojon,malicious ma use hota ha
...bypass inturuson detection system.
but detected easily
nmap -vv (verbose output) <IP>
nmap -A aggressive scan its coombined three scans (os scan,default scirpt engine,versions).....
nmap -p to define port
nmap -p- all the ports
nmap -sV service version detection
nmap -F (fast scan) <IP>
nmap -f (fragmented scan)
nmap - mtu 16 <T> fragmention to 16 bits
![[Screenshot 2025-07-24 114604.png]]
 (Explain this how fragmentation occurs and how header sent or not fullu monimum and max haeader size and all the other important thigs related to  mtu and fragemntation )

nmap -D Rnd :16 <IP>
nmap -S (forge the ip ) <spoof ip> <target>
nmap -sI zombie attack.....
nmap --source-port 53 (forge your port)
nmap --spoof-mac <mac> <T>
nmap --spoof-mac o <T>
nmap -sT -pN -spoof-mac o<T>
nmap --data-length 50 <T>
nmap --randomize-host <T>
nmap --badsum <T>
nmap -sT <T> (TCP FULL SCAN
nmap -sn -PY <IP> SCTP 
custom packets:
its is a window software that is used   to fragment packet colaspft packet builder  (RUN AS ADMIN)
we can send arp,tcp,udp,ip 
1 req 2 response icmp protocal 1
Bannes babbimg

+wmat os is roning
Actie bann er Craabing:
Special claMted Pačketa
Then we conpoue witl databay.
How Tcr/IP Kock wohks.
Passivebanner Lisabing:
y Emoh menajes typo of server, DS, ssL tol.
Snifing te melionsk taaffic
toumu ghabuy Lou peye enttnsa
IdSetve. (which Technologyy Sesver USug).
NelCsaft (Use for bamu grablon
net cat ( Banner) .(surss Aomy knife Tef /IP)
ZT> Pont> a vebbose


-Effechve hort discovery.
-ICMP echo Keqvest

ELITR

cut commanol cot -J " , " -f4,4 zfl.td7.
4'huerts Eh), Doe, 18, Compul u-
FA Fa
F3 F4.

C

Lyis the deliwoes.
nmap LIP> -sn OA host -PE
-- pattet-taace
L, Jhus all percket seid El, To shop port Samins

-- season ( whg nmap saidl sun tasfet ahe)

ICNP timestam zequest (-PP)
nmop LIP> -sn 6A host -PE -- packel -t&ae
-- disabk-apping

Hiah lwel cowmanol

8 pobe

93/ host forol.

+Timesamp

-PE -PS&D -PS443 -PP - PUy01- -PS 3381 - PA21.
~ Pu 161

-- SoubCe-Dort 53.



OPen -Connectioy

it mouy be TEP, UDA SOrp
Closed Back witn es T , TongctUrs ialive /Daad.
Filtered No netpona faowi target , eithe, open /closcd.
vufittaed pOuty TcP-Ack -twe can acces-seities open/closet
open | fteredNo sespone fom specift cont -Fireunll Paotecti on-
csed fltued -onyt in ip idle ciows imponille to dotenuse.

an ce

scau poat is closed or Poltuc bu & Lnwucl

ap-pig

ICMP echo

Nmap -Windau Srau :
-SW (window &cew).
+ It dend YN Paelet and tn marc:
open z Mua0 gets SYNACK (kolmd) gdt RST utth 0 window
Close : biet RST wtth + uplow Si2e.

Size

Dltued, Nwap no hescono ( or get aur mmases.
Maimon- Scan:
Tu's san gend TcP Packets with flo
EIN and Ack and acc to aole if a aut
Mate pocket seceied we sent a esT

221.

pcket baek.


Usiel- Malmaur
Discoverd may BSD -Derved . Sy shen
Silieuryy drop packels.
Closcel- Seut eST Paclel

ELITE

tos best fozmeitting lize a
hepost xsltapoc is oseol

aSltphoc taget. aml -otarget . htu?

check status
Use statebon Ho : Checkn Status
nmap IP p- sV -- gats-evy=5s

Aftu Ss .
Sustem odmini can coufiqse Setvces to
hot sendss bannets, ds to senel s leadyy
ones-lus is &wsity pooutice -
Banwr hrabiadelense






nmap -S :- V F -- siondelay Ss 2IP7.

delay

( Time between Dakets)
Foll Steathy 15s'

pes paocvet

71 - sneaky

nmap - Ty - sS

Nmap Seipting eugie: NSE (l-lanyueg).
owtmate wide varieh of tarks.

enumeresho, lisrovey bovetforce ebl

Vse sorre souting ( Ye path fodlow kao) (No kan Path)
Connect In paory
Nessus (Cowvesicial Rrocte ct).

DeenVAS
LAN Stale mo-
 nikto

Detect Ftewallm
-f (fo< fnagmentsken), 20byfes 6cbts

> nmap _Pn -sS -sV
eso =doda-terty
200 0 10 100.23 4 10.10 23-1 TagdP
- -9(Used

p Router defeaut aabzus
-D Decoy it dliffeent faom spoofing
LApki Tr po clupa dete h
baki IPg ke seh. OT
optimiing nmaD sians :
T o (skallert) -T 5 (Hhahrt

-- scan-delay ( specify amount tme coch
Pacleet senl)

Ss:1m;2h
iue spedf tme to ench host
DowtLow 400 mwc

Fibewall Dolection & IDS Evasin:

ELITA

Pemo Spo

to chante spoofed |port

-- host -Hmcout ztme
Mmap -Su -sS -F -- hos-timout




in wlu'ch we ose wiresha. and
nelcat command,
Syntax:
open wireshak.
host L TargetiP> place as a Liltes.
- start copture.
gnd: mc -nv Taget IP>LPOAt > 192469.0.0 a5
connethon ettaumed then wit
open wreshaktep.post eg 2s os smtp

Then took for yous packet whie
Stutce IP zTIP, and Destnatiol
yors AIP > Lool fn packet weth.
[PSH, ACK ]
and in ne end just fox krowledge
we alwo oseel topolume trrtcaol L
wireghask.

Toovescome dis we ose a technqve.




