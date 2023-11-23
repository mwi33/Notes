# Running snap applications on kali

## Issue
Snap-confine has elevated permissions and is not confined but should be.  Refusing to continue to avoid permission escalation attacks.

## Cause
?

## Solution

This [solution](https://stackoverflow.com/questions/70053614/snap-confine-has-elevated-permissions-and-is-not-confined-but-should-be-refusin) was found on stack overflow.

~~~ bash

sudo apparmor_parser -r /etc/apparmor.d/*snap-confine*

sudo apparmor_parser -r /var/lib/snapd/apparmor/profiles/snap-confine*

~~~

## Issue
missing profile snap-update-ns.nordpass
Please make sure that the snapd.apparmor service is enabled and started.
snap-update-ns failed with  code 1

## Cause

## Solution


# Tags
#snap
#kali
#snap_confine
#apparmor
