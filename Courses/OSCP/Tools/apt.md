Advanced Package Tool (APT) is a Linux utility used to install, remove and update applications and libraries on Debian and Debian based Linux distributions.

~~~ bash

# checks the apt databse for available updates to installed packages
sudo apt update

# applies the relevant updates
sudo apt upgrade

# install applications that are in the apt database
sudo apt install <package>

# remove an install packaged
sudo apt remove <package>

# list all available packages (including those that are not installed)
sudo apt list

# list installed packages
sudo apt list --installed

# search for packages
sudo apt search <package>

# purge files (removes application configuration files)
sudo apt purge <package>

# install local .deb file
sudo apt install ./<package.deb>


~~~