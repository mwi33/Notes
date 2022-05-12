# File Transfer Protocol
TCP port 20 and 21

Active and passive

Anonymous FTP

Trivial FTP (TFTP) - uses UDP
No user authentication

## Authenticating
todo:  add authentication command

sftpd
~~~ bash

# login to sftpd

ftp [ipaddress]

# once logged in we can see the status
ftp> status

# debuging on

ftp> debug

# packet tracing on

ftp> trace

# get files

ftp> get [file name]

# quit the ftp server

ftp> exit

# upload a file

ftp> put [file path]

~~~

## Download everything from a FTP server
~~~ bash

# this is noisy and suspicious

wget -m --no-passive ftp://anonymous:anonymous@[ip address]

~~~

## 

### nmap ftp scrtips
nmap includes additional scripts which can be used to enumerate targets.  The scripts are stored in '/usrr/share/nmap/scripts'

There are several specific scrtips for FTP:

1. ftp-anon.nse
2. ftp-bounce.nse
3. ftp-brute.nse
4. ftp-libopie.nse
5. ftp-vsftpd-backdoorr.nse
6. ftp-vuln-cve2010-4221.nse

## netcat