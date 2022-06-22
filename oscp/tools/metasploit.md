# Overview of Metasploit Framework (MSF)

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

### Index no
1. Unique identifier
2. Type:
    - Auxiliary
    - 

## Updating Metasploit framwork

MSF is updated using the standard package mangager update/upgrade function

~~~ bash
# updating the Metasploit framework
sudo apt update && apt upgrade -y

~~~

