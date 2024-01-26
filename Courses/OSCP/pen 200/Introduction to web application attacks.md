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
## Tags
#enumeration
#nmap 
#burpsuite
#Wappalyzer
#gobuster
#foxyproxy
#firefoxproxy
#intruder





