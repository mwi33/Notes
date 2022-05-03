TCP port 20 and 21

Active and passive

Anonymous FTP

Trivial FTP (TFTP) - uses UDP
No user authentication

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
