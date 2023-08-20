# Installation


~~~ bash
# install snap
sudo apt install snap

sudo snap install core

# install nordpass from snap
sudo snap install nordpass

# start snap service
systemctl start snapd.apparmor
systemctl enable snapd.apparmor

# make nordpass application executable
cd /
cd /snap/bin
chmod +x nordpass

# start nordpass
./nordpass

~~~