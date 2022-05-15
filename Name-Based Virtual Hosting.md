Name-Based Virtual Bosting (NBVH) is a method for hosting multiple domain names on a single server.  This allows one server to share its resources, such as memory and processor cycles, without requiring all the services to be used my the same hostname.

The webserver checks the domain name provided in the h ost header field of the HTTP request and sends a response according to that.

The /etc/hosts file is used to resolve a hostname into an ip address & thus we will need to add an entry in this file for this domain to enable the browser to resolve the address for unika.htb.

~~~ bash

echo "10.129.8.212 unika.htb" | sudo tee -a /etc/hosts

#  tee read from stdin and write to stdout
# -a append to file

~~~