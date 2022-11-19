The Advanced Package Tool (APT) toolset is used to search for, install, remove and update applicatons on Debian based systems (Kali is a Debian based distribution).

The most important benefit of using a package management system like APT is that it also manages application dependencies (other libraries).  

It is a good practise to routinelly update all applications using APT.

~~~ bash


# this command updates the apt database with applicatons that need to be updated
# nothing is installed or removed with this command

sudo apt update

# using the database that is updated using the command above, apt installs the required update.

sudo apt upgrade

# can also use the upgrade command to upgrade a specific application

sudo apt upgrade metasploit-framework

~~~

## Searching for applicatons

When looking for a specific application we should also use the apt application.  Initially, we search the 'kali linux' repositories.

The search function below, searches the application description rather than the application name/title.  This is why some of the returned results have some applicatons that don't contain the search string.

~~~ bash

# this command checks if the 'pure-ftpd' application is in the local repository
sudo apt-cache search pure-ftpd

~~~

We can explore the applicaton description by passing the package name to the 'apt-show' command.

~~~ bash

apt show resource-agents Package: resource-agents

~~~

## Installing applications

We can install the 'pure-ftpd' application using the APT package manager by using the apt command below:

~~~ bash

# after running the command below we will shown the amount of space required and asked if we would like to proceed
sudo apt install pure-ftpd

~~~

## Removing applications

We can also use 'apt' application to remove installed applications.  There are some options on how this is done, which is shown below:

~~~ bash

# this command removes the pure-ftpd application, including data, however, sometimes leaves behind user configuration files/data

sudo apt remove pure-ftpd

# with the '--purge' flag set, all data, including user configuration data is removed.

sudo apt remove --purge pure-ftpd

# the 'autoremove' flag removes dependencies that are no longer required

sudo apt autoremove

~~~

## Using dpkg

dpkg is the tool that is used to install application, even when using apt.  This is the preferred method when working offline as it does not require an internet connection.  The dpkg method does not install dependecies and these will need to be installed separately.

~~~ bash

# this command installs a dpkg file.

sudo dpkg --install /path/to/.dpkg

~~~

## Scheduled tasks

~~~ bash

# this command dispalys all scheduled tasks.
# the looks in the individual folders (daily, weekly, monthly)

ls -lah /etc/cron*

# the command below shows the contents of the crontab file

crontab -l

~~~

## Scheduling a task


