M## What do I want to know?

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

![[Pasted image 20230827031247.png]]

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
3. AAAA: Also known as a quad A host record, the aaaa record contains the IPv6 address of a host-name (such as www.megacorpone.com);
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


