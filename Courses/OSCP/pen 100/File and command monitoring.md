It is important to be able to monitor files and commands in real-time during a penetration test.  There are two commands, 'tail' and 'watch' that help us to do that.  

The most common use of the 'tail' command is to monitor log file entries as they are written.   For example we may want to monitor the Apache logs to determine if a web server is being contacted by a given client that we are attempting to attack via a client-side exploit.

To do this we could use the 'tail' command.

~~~ bash

sudo tail -f /var/log/apache2/access.log

# the -f option continuously updates the output as the target file grows

# the -n X switch outputs the 'x' number of lines instead of the default of 10

~~~

The 'watch' command is used to run a designated command at regular intervals.  By default it runs every 2 seconds, but we can specify a different interval by using the '-n x' flag, where 'x' is the desired interval.

~~~ bash

watch -n 5 ls

# this command will run the 'ls' command every 5 seconds

~~~