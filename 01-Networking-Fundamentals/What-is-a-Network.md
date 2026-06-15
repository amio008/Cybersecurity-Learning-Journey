
## Definition of a Network

A network refers to two or more computers and electronic devices connected through transmission media to share resources and exchange data. Networks can exist without being connected to the internet, for example - an isolated local area network or LAN.

## Types of network

There are various types of networks which are differentiated based on the amount of the area covered, data transfer speed, latency etc. Most widely known and used 
networks are LAN and WAN.

## LAN

LAN or Local Area Network refers to a network where multiple computers or electronic devices are connected within a small geographic area. LANs have very high
bandwidth ranging from 100 Mbps to over 10 Gbps and low latency. Generally, LANs are owned by single organizations. For example - Ethernet or wifi inside a building 
will be considered as LANs.

## WAN

A WAN or Wide Area Network connects multiple LANs over large geographical areas such as cities, countries or continents. Compared to LANS. WANs have lower bandwidth,
higher latency and are more prone to cyber attacks due to covering a much larger area. WANs depend on leased telecommunications lines such as fibre optics or VPNs.
The internet is the biggest example of a public WAN.

##Client

A client could be a machine or a program. A laptop, desktop, smartphone can be a client. A client program is a program that allows the user to make requests. Such as web browsers, or wordpress or photo editing softwares. A client, overall, either a machine or a program, is an appliance and a way to make results through the web.

## Server
Server is a computer program, strictly speaking. High performance computers are called servers because they run server programs. A single server can server multiple clients at the same time. Multiple servers can be run on a single device or machine. THere are virtual servers like Apache or Mysql. Servers contain web resources, host web applications, store user and program data etc and could serve upto hundreds of thousands of clients.

## Cyber attacks - how attackers move through network
Attackers move through network via lateral movements, which is a technique used to move from one compromised device to others within a network, expanding foothold and looking for high-value targets.

#Stages and methods of cyber attacks
1. Initial access: Phishing emails, malicious links
2. Discovery: nmap, netview, ARP table to find devices, ports, folders
3. Credential theft: keylogging, mimikatz, pass-the-hash to steal username and passwords
4. Privilige escalation: getting admin right
5. Lateral movement: WMI, PsExec, RDP to use stolen creds to access other machines
6. Persistence and repeat: Install backdoorrs, repeat steps 1 to 5.
