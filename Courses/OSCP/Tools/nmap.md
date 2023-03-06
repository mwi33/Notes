# NMAP
nmap official [documentation](https://nmap.org).
## syntax
~~~ bash

nmap <flags> <ip address>

~~~

## scripting
nmap comes with a suite of scripts that can be utilised for enumerating targets.

The scripts are stored in the '/usr/share/nmap/scripts'

~~~ bash

nmap --script <script name> <target ip>

~~~


## Common flags (basic)

|flag|name|description|example|
|----|----|----|--------|
|-p|port|scans a specified port|nmap 192.168.1.0 -p 81|
|-sS|TCP SYN|Stealth scan|nmap 192.168.1.0 -sS|
|-Pn|disable ping|Skips the nmap discovery stage and useful for scanning targets with heavy firewall protection|nmap 192.168.1.0 -p 81|
|-v|verbosity|Increases the amount of information shown during a scan|nmap 192.168.1.0 -v|
|--packet-trace|packet trace|Causes nmap to print a summary of every packet sent or received|nmap 192.168.1.0 --packet-trace|
|-sT|TCP connect scan|Uses the system call of the sanme name to scan machines.|nmap 192.168.1.0 -sT|
|-sU|UDP|UDP port scan|nmap 192.168.1.0 -sU|
|-sA|TCP ACK Scan|ACK scan is used to map out firewall rules.  Cannot distinguish between open and closed ports|nmap 192.168.1.0 -sA|
|-sW|TCP Window Scan|Same as an ACK scan however it can detect open and closed scans|nmap 192.168.1.0 -sW|
|-oN|Normal Output|Write output to a specified text file|nmap 192.168.1.0 -oN nmap_output.txt|
|-oG|Grepable formay|output is structred to support grep processing|nmap 192.168.1.0 -oG|
|-sC|default scripts|Uses the default NSE scripts|nmap 192.168.1.0 -sC|
|--min-rate|Minimum number of packets per second|Speeds up the scan as the number increases|nmap 192.168.1.0 -sC|
|-p-|UDP|UDP port scan|nmap 192.168.1.0 -sU|
|-sU|UDP|UDP port scan|nmap 192.168.1.0 -sU|

## Initial scan
The initial scan should be used to identify open ports, services, Operating system and versions.

Subsequenty scan may be used to identify more detail about the implementation of identified systems and any know vulnerabilities.

## 


