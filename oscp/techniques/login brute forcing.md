# HTTP specification
## HTTP authentication
HTTP authentication is used to authenticate the user to the HTTP server.
Basic Authentication uses Base64 encoding to transmit identifier and password.

## Proxy server authentication
Proxy server authentication is used to authenticate the user to an intermediate proxy server.

## HTTP headers
1.  WWW-Authenticate
2.  Authorization header field

## HTTP response codes
1.  2xx
2. 401 - Unauthorised
---
# Cracking passwords
## Methods
1.  Online brute force attack - Over a network using http, https, ssh, ftp, sftp.
2. Offline brute force attack - Cracking a password hash.
3. Reverse brute force attack - Using a single password with a list of usernames.
4. Hybrid brute force attack - Creating a customised password list based on intelligence of the target user.
## Password attack types (brute-force)
1. Dictionary attack - Uses a list of know passwords
2. Brute force - Checking every possible password
3. Traffic interception
4. Man in the middle
5. Key logging
6. Social  engineering

## Calculating the number of possible passwords
The number of possible passwords can be calcuated by raising the password space to the power of the password length.

Password space is how many characters can be used i.e. just lowercase letters has a password space of 26.

Number of characters is how many characters are in the password i.e. 4
26^4 = 456,976 possible passwords.

---
# Brute forcing login forms

# Default passwords
These are the passwords that are provided with a device for initial authentication.  It is intended that these are changed as part of the installation/implementation of the device.  Often these are not changed.

---
# Tools
1. Ncrack
2. wfuzz
3. medusa
4. patator
5. hydra

## Hydra
Common flags
~~~ bash
-C combined username:password list
-L username wordlists
-l set a fixed username
-P Password wordlist
-p set a fixed password
-f stop after successful login
-s port

~~~

Hydra command structure
~~~ bash
	# -C  --> Combined credential word list
	# Target IP
	# -s --> target IP port
	# http-get --> request method
	# / --> target path
	 
hydra -C <type of wordlists> <wordlist path(s)> <target IP Address>  -s <target port> <target http-method (get)> < target path (/)> 

hydra -C /usr/share/wordlist/ftp_username_password.txt 192.168.1.1 -s 21 http-get /

~~~

Hydra http(s)-post-form module.  Defining the success/fail string is important and possibly not obvious.  Using the absence of the 'log-in form' as an indication that we have logged in successfully should work.  The logic being that once you are logged in, the 'log-in' form will no longer be relevant.

The formatting of the fail/success string is 

~~~ bash

F=html_content
S=html_content

# worked example

:F=<form name='login'>

~~~

~~~ bash

# hydra <module> <url path> <post parameters> <success/fail string>

hydra http-post-form/login.php:[user parameter]=^user^&[password parameter]=^pass^:[success/fail string]

~~~
# hydra http-get

~~~ bash

hydra -C <path to username and password list> <IP address> -s <port> http-get /

# / the slash is the path to the login page

~~~
---
# hydra http-post-form

~~~ bash
#
# the syntax for a form attack is similar to a standard http-get.  http-post-form is followed by 3 parameteres separated by ':'
# These are:
# /the path to the login page
# the structre of the username & password post parameter with place holders where the username and password from a wordlist are inserted t.o test the form
# e.g.  username=^USER^&password^PASS^.  username and password componetes are obtained from the http-post message (developer tools or burp.
# ^user^ and ^PASS^ are placeholders where data from respective word/password lists are inserted into the HTTP message.


hydra -l <user name> -p <password> -f <IP address> -s port http-post-form "/login.php:username=^USER^&password=^PASS^:F=<form name='login'"

~~~

---
# Password spraying
Password spraying is essentially the re-use of already cracked passwords from the same target and checking if they work on administrator portal/logins.

---
# Resources
1.  [SecList](https://github.com/danielmiessler/SecLists) - Multiple types of lists used for security assessments.
2. 