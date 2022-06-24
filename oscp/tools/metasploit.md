# Metasploit Framework (MSF)

At the core of MSF is the MSF project.  The project has two implementations: the Metasploit Pro and Metasploit Framework.  There are several differences, the most obvious being that Metasploit Pro includes a GUI.

The msfconcolse is probably the most popular interface to the Metasploit framework.

The files for the MSF are included in the /usr/share/metasploit-framework directory.  This directory and the framework in general composed of the following components:

1.  Data, Documentation and Lib - These are the basefiles for the framework.  This is what the msfconcole interfances with;
2.  Modules - Modules are organised into separate categories; auxiliary, encoders, evasion, exploits, nops, payloads and post;
3.  Plugins - Plugins provide additional flexibility and support additional functionally and automation;
4.  Scripts; and
5.  Tools.

---

## Starting msfconsole

To start the msfconsole type msfconsole into to a terminal.

~~~ bash

# start the console
msfconsole

# start the concolse without the banner
msfconsole -q

~~~
---
## Modules
Modules are prepared scripts with a specific purpose.

From within the framwork (console), the following sytax is used to select modules:

~~~ bash

# Pseudo code
<no .> <type>/<os>/<service>/<name>/

# worked example

794 exploit/windows/ftp/scriptftp_listS

~~~

### Module parameters

1. Index no
2. Unique identifier
3. Type:
    - Auxiliary
    - Encoders
    - Exploits
    - NOPs
    - Payloads
    - Plugins
    - Post
4. OS (operating system)
5. Service
6. Name (the name tag explains the actual action that will be undertaken by the module)

---

## Searching for a module
From within the msfconsole we can search for modules using these tags.

~~~ bash

msf6 > search help

~~~

---

## Searching for an exploit

~~~ bash

msf6 > eternalromance

~~~

---

## Using msf

~~~ bash

msf > use <index no>

~~~

---

## Updating Metasploit framwork

MSF is updated using the standard package mangager update/upgrade function
