## Users and groups
~~~ bash

cat /etc/passwd

john:x:1002:1002:John Doe,,,:/home/john:/bin/bash

# this returns a colon separated string.  Details of this are below
~~~

|Item|Description|Example|
|----|------------|---------|
|1|Username|john|
|2|Indicates that the hashed password is storedin the /etc/shadow/|x|
|3|User id|1002|
|4|Group id|1002|
|5|Comments|John Doe|
|6|Comments|John Doe|
|7|Comments|John Doe|
|8|Comments|John Doe|
|9|Home directory|/home/john|
|10|Shell environment|/bin/bash|

### Adding and removing new users

~~~ bash

sudo useradd --home /zeldahome --shell /bin/bash zelda

sudo userdel --remove zelda

~~~

## File permissions
Each file or directory has specific permissions for three categories of users:

* its owner (u - user);
* its owner group (g), this represents all users in the group; and
* the others (o).

In addition to this, three types of rights can be applied (combined):

* read (r);
* write (w); and
* execute (x).

The second way to represent permissions is via an octal numeric representation.  The method associates a permission with a value:

* 4 for read;
* 2 for write; and
* 1 for execute.

We can associate the sum of these to the combination of permissions:

* 1 - execute ;
* 2 - write ;
* 3 - write and execute;
* 4 - read;
* 5 - read and execute;
* 6 - read and write; and
* 7 - read, write and execute.

0 means that there are now permissions.

### Files
For files this model is simple to follow; read means the user can read the file, write means that the user can modify it and execute means that it can be run, which implies that it is executable (a program).

### Directories
Directories are handled differently.  Read access allows the user to consult a list of the directory contents. Write access allows the user to create and delete files and directories within the parent directory.  Execute means that the user can cross through the directory to access its contents.  Being able to cross through a directory without being able to read it gives the user permission to access known enteries, but only by knowing their exact name.

~~~ bash
# using the long option on the ls command provides the permissions of the contents of a directory

ls -l 

~~~



### Changing permissions and ownership
We can use the 'chown' command to change the permissions of a file or directory and both representations can be used to change the required permissions.

#### Change Ownership

~~~ bash
# change the owner for a file.  This requires elevated priviliges
# sudo chown [user] file

sudo chown root test_file.txt

~~~

#### Change Permissions

~~~ bash

# chmod priv_user, priv_group, priv_other [file_path]

# u - user
# g - group
# o - other

# r - Read
# w - Write
# x - eXecutable

chmod u+x, g+w, o-r file.txt

# chmod owner,group,other

chmod 754 file.txt

# read, write execute for the owner
# read, execute for the group
# read only for others

~~~

## SETUID, SETGID and the Sticky bit

SETUID and SETGID are special permissions that pertain to execuatables.  These are represented by the letter 's'.  

's' in the user space means that both the execute and SETUID flags are set.  A 'S' would mean that the SETUID flag is set by the execute flag isn't.

~~~ bash

# change the user owner to root

sudo chown root:kali /usr/bin/idcopy

# set the SETUID flag 's'

sudo chmod u+s /usr/bin/idcopy

# the idcopy command is now executed with root privileges

# this command now has a euid (effective user id) of  0 - root

~~~

This method can be used as part of a path injection exploit.

### Searching for files with SETUID or SETGID

~~~ bash

# how to search for files with the SETUID or SETGID bit set

find / -perm -u=s -type f 2>/dev/null


~~~

## Linux processes

PID = process id.  Each time we run a program from the terminal the kernel starts a new process.  

Linux also contains the concept of jobs.  

~~~ bash

# the following contains a pipline of two process which linux considers a single 
# job

cat errot.txt | wc -m


~~~

Jobs can be controlled, that is to suspend and restart as required.

Jobs running in the foreground consume the terminal instance and no other commands can be run.  These jobs can be sent to the background to recover the terminal. 

Processes can be run in the background by add the '&' to the end of the command.  This means that the processes runs in the background and the terminal can still be used.

The following code block includes this and other commands that can be used with background processes.

~~~ bash

# runs the command in the foreground

ping -c 400 localhost > ping_results.txt

# this command writes the output of the ping command to a text file

ping -c 400 localhost > ping_results.txt &

# this does the same thing, however, runs the process in the background 

~~~


ctrl+Z can be used to suspend a processes.   The 'jobs' command lists all of the current jobs with the following data:

%number - the job number
%string - the name of the job (%ping)
%+ or %- refers to the current job
%- - refers to the previous job

The 'fg' command returns a process to the foreground.

### Listing linux process

It is useful to be able to list linux processes.  This can be done from the terminal by running the following command.

~~~ bash

# list all running processes
ps -ef

~~~

Its very useful to be able to list all of the current processes running on a machine.  The 'ps' command does this.

~~~ bash

# this command lists all of the currerntly running processes.
# the 'e' flag selects all processes
# the 'f' flag prints the full format listing

ps -ef

# to search for a specific process the 'f' and 'c' flags can be combined with the name of the relevant process

ps -fc terminator

# the 'c' select a preferred processes/command

# processes can be stopped using the 'kill' command and the process id (PID)

kill 1307

~~~

