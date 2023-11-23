n# Table of Contents
1. What do I need to Know
2. The Penetration Testing Life-Cycle
3. Passive Information Gathering
	1. Tools and techniques
		1. Whois enumeration
		2. Google hacking
			1. Dork search portal
		3. Netcraft
		4. Open source code
		5. Gitrob and Gitleaks
		6. Shodan
		7. Security Headers and SSL/TLS
	2. Active Information Gathering
		1. DNS Enumeration
			1. DNSRecon
			2. DNSenum
			3. Windows nslookup
		2. TCP/UDP Port Scanning Theory
			1. NMAP
			2. NMAP scanning techniques
				1. SYN (stealth) Scan
				2. TCP Connect Scan
				3. UDP Scan
## What do I want to know?
1. What tools should I use?
2. Are their standard scans that I should use?
3. What does information scanning provide in notes and documentation?
4. How to I remain anonymous?
5. How much should I apply OSINT?
6. Should I use Maltego?
7. What types of scans are legal?
8. Scanning technique/process
9. What should my initial scans look like
10. Creating and retaining scan logs
11. How to be anonymous
## The Penetration Testing Life-cycle
The penetration testing life-cycle is applied each time a pen test is conducted.  The life-cycle is:
1. Defining the scope;
2. Information scanning (enumeration);
3. Vulnerability detection;
4. Initial foothold;
5. Privilege escalation;
6. Lateral movement;
7. Reporting/analysis; and
8. Lessons learnt/remediation.

The scope of a pen test normally includes the IP range, machines and applications that should be include.  Sometimes, other items are called out specifically as out of scope.  Pen testers should be cautious about included machines or application that are not specifically called out as in-scope.

Information gathering starts with reconnaissance to retrieve details about the target organisation's infrastructure, assets and personnel.  This can be done passively or actively.  

Active information gathers generally reveals a larger footprint. 

Information gathering will normally continue through the life-cycle and as new items are discovered they are added to the larger picture.
## Passive Information Gathering
Information gathering is often referred to as 'enumeration'  and passive information gathering is called Open Source Intelligence (OSINT).  OSINT is the processes of collecting publicly available information, often without interacting with the target.  

There are two different interpretations.  Firstly, that at no time do we directly interact with the target and information gathering is only through indirect methods.

The other interpretation is that we can interact with the target using functions that are open to other users.  We could for example, navigate to a website, create an account e.t.c.

When deciding which interpretation we will apply, we would refer to either the scope and rules of engagement.

The objective of information gathering is to develop and refine the targets 'attack surface'.  This view can assist us in developing phishing campaigns, guessing passwords and account compromise.
### Tools and techniques
#### whois enumeration
whois is a TCP service tool and database that can provide information about a domain name like name server and registrar.  

In a forward search, a domain name is provided and the IP address is returned as well other information including name servers.   A reverse lookup is the opposite.  A IP address is provided and domain names are returned.
#### Google Hacking
Google hacking is essentially to uese specific search commands to refine searches.  As an example, a search can be limited to a specific domain by using the following command.

~~~ bash
# limits results to a singular domain (and subdomains)
site:megacorpone

# limits results to only text files
filetype:txt

# this excludes results that have the provided argument
-filetype: html

# use quotes where there is whitespace
# note that multiple arguments can be used.  This case retuns results that have 
# "index of" in the title and "parent directory" on the page
intitle:"index of" "parent directory"

~~~

The image below provides and example of a directory listing, which if improperly implemented can provide a list of interesting files and sensitive information.

The [Google Hacking DB](https://www.exploit-db.com/google-hacking-database) provide a useful resource of google search operators which can be used for collection of information.
##### Dork Search Portal
The '[Dork Search Portal](https://dorksearch.com)' provides a pre-built list of subset of queries and a builder to construct searches.  
#### Netcraft
Netcraft is an English web portal that provides information related to the tech stack for a give website and which other hosts share the same IP netblock
#### Open Source Code
Some google search operators will work on some open-source code repositories.  The example in the 'Offensive Security' documentation uses the 'filename' qualifier, however, this has been replaced with 'path'.

The search string should be constructed as shown below:

~~~ bash

# this is the search string for looking for files that have user in the name and in the repository 'megaonecorp'.

repo:megacorpone/megacorpone.com path:user

# this search stirng returns a single file 'xampp.users'

trivera:$apr1$A0vSKwao$GV3sgGAj53j.c3GkS4oUC0

~~~

#### gitrob and gitleaks
[gitrob](https://github.com/michenriksen/gitrob) is a command line application that.......
[gitleaks](https://github.com/gitleaks/gitleaks) is a command line application that....
#### shodan
Shodan is an internet search engine that scans for internet connected devices, in particular IOT.  This is very useful for searching a domain for devices that are connected for the same IP block.  It is passive as we do not directly interact with the target.
#### Security Headers and SSL/TLS
[Security Headers](https://securityheaders.com) is a website that scans the http headers to make an assessment of an organisations security posture.

[Qualys SSL/TLS](https://www.ssllabs.com/) is a website that checks the implementation of SSL/TLS and provides information regarding potential vulnerabilities.  This site also includes implementation advice for SSL and TLS.

## Active Information Gathering
This section includes a concept called living off the land.  Essentially, this means that our engagement requires us to use a desktop machine provided by the client.  Typically, this is a standard Windows based machine, which has limited tools.

Some useful tools (binaries) exist on a windows machines.  These are referred to as LOLBins or LOLBAS (binaries, scrips and tools).
#### DNS Enumeration
The Domain Name System (DNS) is a distributed database responsible for translating user-friendly domain names into IP addresses.  This is facilitated by a hierarchical structure that is divided into several zones, starting with the top level (root) zone.

Each domain can use different types of DNS records.  Some of the most common types of DNS records include:

1.  NS: Name server records contain the name of the authoritative servers hosting the DNS records for the domain;
2. A: Also known as a host record, the 'a record' contains the IPv4 address of host-name (such as www.megacorpone.com);
3. AAAA: Also known as a quad A host record, the a record contains the IPv6 address of a host-name (such as www.megacorpone.com);
4. MX: Mail exchange records contain the names of the servers responsible for handling email for the domain.  A domain can contain multiple MX records;
5. PTR: Pointer Records are used in reverse lookup zones and can find the records associated with an IP address;
6. CNAME: Canonical Name Records are used to create aliases for other host records; and
7. TXT: Text records can contain any arbitrary data and be used for various purposes, such as domain ownership verification.

Due to the large amounts of data held within the DNS it is a lucrative target for active information gathering.  The 'host' command can be used to retrieve some of this:

~~~ bash
host www.megacorpone.com
megacorpone.com has address 149.56.244.87

host -t mx www.megacorpone.com
megacorpone.com mail is handled by 10 fb.mail.gandi.net
megacorpone.com mail is handled by 20 spool.mail.gandi.net
megacorpone.com mail is handled by 50 mail.megacorpone.com
megacorpone.com mail is handled by 60 mail2.megacorpone

# we can check for a subdomain by running the following command

host idontexist.megacorpone.com

Host idontexist.megacorpone.com not found: 3(NXDOMAIN)
~~~

We can see that there is a specific error code '3(NSDOMAIN)' returned when there isn't a record that matches.  We can use this to automate checking for domains.  If a host successfully resolves a name to an IP address, this could be an indication of a functional server.

We can use a simple word list with common host names and check if there is a valid DNS record.

~~~ bash
cat list.txt
www
ftp
mail
owa
proxy
router

for ip in $(cat list.txt); do host $ip.megacorpone.com; domnw

# this add each of the items in the 'list.txt' document to check if each has a #valid dns record.

host www.megacorpone.com
# this would return a positive result

host ftp.megacorpone.com
# this would return a negative result
~~~

This technique can be used with much more comprehensive word lists.  There is a collection of much more comprehensive word lists available through the 'SecLists' project.

It can be installed using the 'apt' application manager

~~~ bash
# install the SecLists datasets
sudo apt update seclists
~~~

As we have found several IP addresses in a specific range, we can create a loop to apply a reverse lookup to check for domain names within a certain range.

~~~ bash
# uses a single line bash script to check all IP addresses in a sequence.
# this is a reverse lookup to identify names
for ip in $(seq 200 254); do host 51.22.169.$ip; done | grep -v "not found"
~~~

This returns a lot of results which represents several IP address to valid domains.  If this was an in depth analysis, each of these domains would be further investigated.
##### DNSRecon
DNSRecon can be used to automate the process of enumerating DNS records.  The examples below include both a initial (standard) scan and a brute force using the simple word list.

~~~ bash
# initial DNS scan
dnsrecon -d megacorpone.com -t std

# brute force domains using a word list
dnsrecon -d megacorpone.com -D list.txt -t brt
~~~

##### DNSenum
DNSenum is a populate tool that can be used to further automate DNS enumeration.  

~~~ bash
# initial DNS scan
dnsenum megacorpone.com
~~~

The command above returns additional domains that we have previously identified.  
##### Windows nslookup
On a Windows machine, the 'nslookup'  (LOLBAS) is a useful tool and operates in a similar way as the Linux tools (host, DNSRecon and DNSenum) above.  

~~~ bash
# here we resolve the A record for the mail server
nslook megacorpone.com

# this is a more granular scan to explore any TXT records
nslook -type=TXT info.megacorpone.com
~~~

#### TCP/UDP Port Scanning Theory
Port scanning is the process of scanning remote machines to identify what ports, services and versions are running on a target.  This can lead to the identification of attack vectors.

>Port scanning can be considered illegal and should only be conducted in lab environments or with written permission.

Port scanning can generate a lot of traffic and in some instances could create downtime for the owner.

There is a distinction between scanning a target and scanning a port.  It is good practice to scan common ports first (80 and 443) first and then scanning these ports specifically.

It is important to remember that initial scans is to develop a high-level understanding of the target, which is then further developed my undertaking more direct scans of a particular port.

At the high level, port scanning a client sends a TCP SYN packet on a target port.  If the destination port is open the target responds with a SYN-ACK packet.  The client then sends and ACK packet to complete the handshake.  If this is successful, the port is considered open.

We can use 'net cat' to run simple port scans.  Whilst this is not the primary use for 'net cat', it is a useful choice as it is readily available on most servers.

~~~ bash
# this command uses netcat to run a simple port scan on ports 3380 to 3390
# this is a TCP scan
nc -nvv -w 1 -z IP 3388-3390

nc --> use the net cat application
-n --> numeric only IP address, no DNS
-vv --> verbosity.  Add more v to be more vebose
-w --> timeout in secods for connects and final net reads
-z --> zero-I/O mode used for scanning

~~~

~~~ bash
# this command uses netcat to run a simple port scan on ports 120-123
# this is a UDP scan

nc -nv -u -z -w 1 IP 120-123

-u --> UDP scan
~~~

An ICMP response indicates that a port is closed.  Open ports have the packet passes to the application layer and responses here are based on how the application has been implemented to respond to empty packets.

UDP scanning can be unreliable as a 'non response' indicates an open port.  If a firewall is in place a response will indicate an open port, however, it could be that the firewall has not either passed the empty packet to the application or not respond at all.
##### NMAP
[nmap](https://nmap.org/) is a popular open source network scanner that has been under development for more than two decades.  

It is important to understand the footprint (network traffic) that each scan creates.  We can measure this using [IP tables](https://en.wikipedia.org/wiki/Iptables) 
Below we scan a lab machine while monitoring the traffic with 'iptables'.  

~~~ bash
# this command creates the 'INPUT' rule followed by the rule number
sudo iptables -I INPUT 1 -s [IP address] -j ACCEPT

# this command creates the 'OUTPUT' rule followed by the rule number
sudo iptables -I OUTPUT 1 -s [IP address] -j ACCEPT

# this command zeros the packet and byte count
sudo iptables -z

# this command shows the traffic captured through the 'ip tables' chains (rules)
sudo iptables -vn -L

-vn adds verbosity and numeric output
-L lists the rules present in all chains

~~~

A default TCP scan will check the top 1000 ports and generates about 100 KB of traffic.  A more thorough scan, testing all 65000 ports generates nearly 4 MB of traffic, which is significantly more traffic, however, identified more open ports.


~~~ bash
# standard nmap scan of the top 1000 ports
# this scan generates anout 100k of network traffic
nmap 192.168.212.151

# this scan, scans all 1-655355 ports and generates about 4mb of network traffic
nmap -p 1-655355 192.161.212.151
~~~

NMAP has several types of scans, including the SYN scan (stealth scan).  This is the standard scan if no other parameters are passed to the application.  It does however require 'raw socket' privileges.  This scan does not send the final 'ACK' packet and therefore does not complete the 3 way handshake.  This means that the packet never gets passed to the 'application layer' and therefore won't appear in any application logs.

~~~ bash
# standard nmap scan (SYN/Stealth)
sudo nmap 192.168.212.151
~~~

When a user does not have 'raw socket' privileges, the nmap will default to the standard 'TCP connect' scan.  A TCP connect scan is slower than other scan types as it waits to complete the handshake before indicating that the port is open.
the TCP connect scan is often used when scanning through proxy.

~~~ bash
# a typical TCP connect scan
nmap -sT 192.168.212.151
~~~

UDP scans use two different methods to determine if  a port is open or closed.  It will use a standard ICMP port unreachable and a for common ports it will use a protocol specific SNMP packet.  This scanning type requires that the packet is provided to the application and receives a application packet responsive.

~~~ bash
# a typical UDP scan uses the format below
sudo nmap -sU 192.168.212.151

# this scan type can be used with TCP syn scan
# this scan provides a more complete picture 
sudo nmap -sU -sS 192.168.212.151

# we can scan multiple ports using the --top-ports paramater
# the -A paramater includes a trace-route
sudo nmap -sT -A --top-ports=20 192.168.212.151 -oG top-port-sweep.txt

~~~

Network sweeping techniques involves starting with broad scans and then narrow down scanning to specific hosts of interests.
Frequently, it is useful to be able to review the scan logs to understand the landscape of available ports.  We can use the -oG flag to write the output to a file in a 'greppable' format.
The '-o' flag indicates an output, followed by another attribute '-oG' for greppable.  These can be found on the [NMAP](https://nmap.org/book/man-output.html) site.

NMAP has a function to identify the OS on a given target.  This is enabled by using -O parameter.  This is essentially a fingerprinting exercise which is accomplished by inspecting the returned packets.

A full NMAP scan of a class c network with 254 hosts would create 1000 MB of network traffic.  
##### NMAP scanning techniques
###### SYN (stealth) Scan
SYN scanning is the default TCP scan, which requires raw socket privileges.  SYN scans send SYN packets to various ports and open ports send a SYN ACK is returned.  The SYN scan then flags that port as open.  The three way handshake is never completed.

~~~ bash
# standard SYN (stealth) scan is the default scan and requires raw socket privileges

sudo nmap -sS 192.168.212.151
~~~

Because the three way handshake isn't  completed the packet is never sent to the application layer, consequently it doesn't appear in any application logs.  Additionally, it is faster as less packets are sent.
###### TCP Connect Scanning 
This scanning technique completes a full TCP connection.  It is the default scanning type if the user does not raw socket privileges.  This type of scan is generally slower as it must wait to complete the three way handshake.  It is considerably slower than a SYN (stealth) scan.   This scan is useful when navigating a proxy.   

~~~ bash
# a standard TCP Connect scan is the default scan for users who do not have raw socket priviliges.

nmap -sT 192.168.212.151
~~~
###### UDP Scanning
UDP scanning uses two different methods to determine if a port is open or closed.  For most circumstances it will use a standard 'ICMP port unreachable method' by sending an empty packet to a given port.  

However, for some common ports it will use a protocol specific port.  For example, for port 161 (SNMP), a packet designed to be processed by an application bound to that port.

~~~ bash
# to perform a UDP scan we use the -sU.  SUDO is required for raw socket access.

sudo nmap -sU 192.168.212.151
~~~

Both TCP SYN and UDP scans can be used in conjunction with each other for a more complete picture of the target.

~~~ bash
# joint TCP SYS and UDP scan

sudo nmap -sS -sU 192.168.212.151
~~~

With this information we can now conduct a 'network sweep' scan for identifying hosts.  During a 'network sweep' scan, NMAP also sends TCP SYN packet to port 445, a TCP ACK packet to port 80, and an ICMP timestamp request to verify whether  a host is available.

~~~ bash
# nmap network sweep
namp -sn 192.168.212.151
~~~

It is important that records of scans are kept in an organised and accessible manager.  Fortunately, nmap has the ability to provide output files which can be analysed.  The -o parameter is used to write the scan output to a file.
It is used with a second parameter to define the type of output. 

~~~ bash
# the output files are:

# interactive output.  This is the standard output using the stdout and is read # from the command line.

# normal output is similar to the interactive output in that it uses the stdout  # to write to the command line, however, it also writes to a file of you choosing
nmap -sT -oN output.txt 192.168.212.151

# xml output is useful as it is written in a structured way and can be parsed by # several different programing and scripting languages
nmap -sT -oX output.txt 192.168.212.151

# grepable output is a simple output that makes it easy to analyse using        # standard command line tools like grep, awk, cut and diff.
nmap -sT -oG output.txt 192.168.212.151

# Script Kiddie most likely a easter egg......definately worth trying
nmap -sT -oS output.txt 192.168.212.151
~~~

NMAP can be used for scanning only specific ports, which can reveal more data about certain services running and reduce the time taken by limiting the number of packets that are sent.

~~~ bash
# the command below scans only port 80 and provides more detail about the services running on that port and prints the output to a grepable format
nmap -p 80 192.168.212.151 -oG web-sweep.txt

# we can further refine out scan by scanning the top 20 ports, OS detection, script scanning and traceroute
nmap -sT -A --top-ports=20 192.168.212.151 -oG top-port-sweep.txt

~~~

The 20 NMAP ports are determined using the /usr/share/nmap/nmap-services file, which uses a simple format of three white space-separated columns.

NMAP has the ability to identify operating systems based on know fingerprints.  This is set with the -O parameter.  NMAP normally only shows the operating system if it meets certain criteria, however, we can force NMAP to display the operating systems regardless of the confidence in the fingerprint.

~~~ bash
# nmap being used to fingerprint OS and printing them regardless of the confidence in identifying them
sudo nmap -O 192.168.212.151 --osscan-guess

# with the OS identified, services can be further explored by examining service banners with the -A parameter.

nmap -sT -A 192.168.212.151

~~~

##### NMAP Scripting Engine
The NMAP Scripting Engine (NSE) provides the capability to automate or customise scanning tasks, including those that are defined/created by the user.

There is a built-in help function which is called by passing the following parameters with the NMAP command

~~~ bash
# nmap scripting engine help
nmap --script-help http-headers
~~~

The NSE can be used for DNS enumeration, brute force attacks and vulnerability identification.  These scripts are located at '/usr/share/nmap/scripts'

a NMAP script is called by using the '--script' flag with the name of the script as a parameter.

The 'http-headers' script attempts to connect to the 'http' services on a target system and determine the supported headers.

~~~ bash
# using the nmap scripting 

PS C:\Users\student> Test-NetConnection -Port 445 192.168.203.52
# this will respond with a message confirming if the tested port

# additionally, we can scritpt checking the first 1024 ports

PS C:\Users\student> 1..1024 | % {echo ((New-Object Net.Socekts.TcpClient).Connect("192.168.50.151", $_)) "TCP port $_ is open"} 2>$null

tcp port 88 is open
~~~

~~~ powershell 
# explore this code

% {echo ((New-Object Net.Socket.TcpClient).Connect("192.168.50.151", $_)) "TCP port $_ is open"
~~~

###### SMB Enumeration

NetBIOS on port 139 as well as several UDP ports.  SMB runs on TCP port 445.  NetBIOS and SMB are two separate protocols.  NetBIOS is an independent session layer protocol and service that allows computers on a local network to communicate with each other.  Whilst SMB can work without NetBIOS, NetBIOS over TCP is required for backward compatibility and these two services often go hand in hand, as such enumeration of these two are often done together.

A nmap scan targeting both SMB and NetBIOS will include both ports.

~~~ bash

nmap -v -p 138,445 -oG smb.txt [IP]

# -v is for verbosity
~~~

Nmap includes several scripts specifically for SMB enumeration.
###### nbtscan
The nbtscan is an application specifically for enumerating NetBIOS.

~~~ bash

sudo nbtscan -r [IP/24]

# -r specifies that local port 137 should be used

~~~

###### Enumerating from Windows

'net view' is included in Windows machines and lists domains, resources and computers belonging to a given host.  We can list all the shares running on a given domain controller.

~~~ bash

net view \\dc01 /all

~~~ 

## Tags
#lifecycle
#deliverables
#osint
#informationgathering
#reconnaissansse
#whois
#dnslookup
#reversednslookup
#googlehacking
#robots
#robotstxt
#netcraft
#techstack
#ip
#netblock
#ipnetblock
#opensourcecode
#shodan
#securityheaders
#rssl
#tls
#implementation
#livingoftheland
#activeinformationgathering
#dnsenumeration
#OWASPPenTestingExecutionStandard 
#dnspointer
#pointer
#cannonical
#bashloops #bashoneline
#bashscripts
#scripts
#rdp
#xfreerdp
#portscanning
#tcp
#udp
#netcraft 
#nc
#handshake
#iptables
#nmap
#synscan
#stealthscan
#tcpconnctscan
#scanwithproxy
#udpscan
#jointtcpudpscan
#networksweep
#smb
#netbios



