## Initial scans
Undertake an initial TCP and UDP scans of the target machines

~~~ bash
sudo nmap [IP] -oG nmap_tcp_initial

sudo nmap [IP] -sU -oG nmap_udp_initial

sudo nmap [IP] -sn -oG nmap_network_sweep

sudo nmap [IP] -O --osscan-guess -oG nmap_os_guess

sudo nmap [IP] -p 22 -oG nmap_tcp_p25

sudo nmap [IP] -p 22 -oG nmap_tcp_p80

sudo nmap [IP] --script ssh2-enum-algos.nse -oG nmap_script_ssh2-enum-algos

sudo nmap [IP] --script ssh-auth-methods.nse -oG nmap_script_ssh-auth-methods

sudo nmap [IP] --script http-enum.nse -oG nmap_script_http-enum

~~~

## Scan results
|port|type|service|status|scan log|notes|
|----|----|-------|------|--------|-----|
|22|tcp|ssh|open|nmap_tcp_initial|none|
|80|tcp|http|open|nmap_tcp_initial|none|
## Users
|username|password|service|hash type|log|free text|
|----|----|-------|------|--------|-----|
|none|none|none|none|none|none|
|none|none|none|none|none|none|
## Operating system
Linux
## Authentication methods
|port|service|authentication method|notes|
|----|-------|----|-----|
|22|ssh|public key|none|
|22|ssh|password|none|
## HTTP enumeration
|url|folder|file|note|
|---|------|----|----|
|[IP]/login.php|N/A|login.php|none|
|[IP]/css/|css|N/A|none|
|[IP]/img/|img|N/A|N/A|none|
|[IP]/js/|js|N/A|none|
|[IP]/lib/|lib|N/A|none|
