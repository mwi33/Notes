# Overview
On Kali (and presumably other linux ) Nordpass is installed using the '
snap' package manager.  Installation is very simple, however, on Kali, the snap package manager needs to be  installed.
When starting Nordpass after installation several errors/privileges.

As there are several different errors , I will document the solution for each of them below.

## Errors
' Snap-confine' has elevated permissions and is not confined but should be.  Refusing to continue to avoid permission escalation attacks.  Please make sure that the snapd.apparmor service is enabled and started..

~~~ bash
# check the status the snapd.apparmor service.  if it isnt started and enabled, start and enable these services

systemctl status snapd.apparmor

# enable the snapd/apparmor

systemctl start snapd.apparmor

# start the snapd/apparmor service

systemctl start snapd.apparmor

~~~