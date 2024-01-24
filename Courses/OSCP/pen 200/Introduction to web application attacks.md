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
## Tags
#nmap 
#burpsuite
#Wappalyzer
#gobuster
#foxyproxy
#firefoxproxy
#intruder





