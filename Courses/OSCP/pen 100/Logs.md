In response to a security breach, logs can be used to reconstruct events and understand what happened.

Perhaps in indication of how important these log files are, many of them cannot be read without root permissions, consequently when we are interacting with these files we often have to use 'sudo'.

Most unix like system produce logs within the 'var/log' directory.

~~~ bash

ls -l /var/log

# we can look at the last three enteries using the 'tail' command

sudo tail -3 /var/log/auth.log

# we can use the who command to read a structured log - 'wtmp'

sudo who /var/log/wtmp | tail -5

~~~

## Kernel logs

The kernel emits messages that it stores in a ring buffer whenever something interesting happens (new USB device inserted, failing HD operation, initial hardware detection on boot).  

~~~ bash

dmesg

# Shows the kernel messages

~~~

# Journalctl

The 'journalctl' command will dump all the available logs chronologically.  With the -r option, it is printed in reverse, meaning that the most recent enteries are shown first.  

The -f option will continiously print new log enteries as they are appended to it's database.

The -u option can limit the output to those emitted by a specific systemd unit.

~~~ bash

# dump all available logs

journalctl

# in reverse order (newest first)

journalctl -r

# continously as they are entered in the database

journalctl -f

# limit output to a certain systemd unit

journalctl -u ssh.service

~~~

Logs are an excellent tool when troubleshooting an unexpected error or event.

## Runlevel

Runlevel is an operating state on linux/unix based systems.  They are numbered from 0-6.  Runlevels determine which programs can execute after the OS boots up.  The runlevel defines the state of the machine after boot.

Runlevels 0,1 and 6 are always the same and 2,3,4 and 5 are different depending on the linux distribution.

|Runlevel|Description|
|--------|-----------|
|0|Shuts down the system|
|1|Single user mode|
|2|Multi user mode without networking|
|3|Multi user mode with networking (with CLI)|
|4|User definable|
|5|Multi user mode with networking (with GUI|
|6|Reboots the system to restart it|


