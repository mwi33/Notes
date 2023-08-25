## What do I want to know?

1. What tools should I use?
2. Are their standard scans that I should use?
3. What does information scanning provide in notes and documentation?
4. How to I remain anonymous?
5. How much should I apply OSINT?
6. Should I use Maltego?
7. What types of scans are legal?

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

In a forward search, a domain name is provided 

## Tags
#lifecycle
#deliverables
#osint
#informationgathering
#reconnaissansse
