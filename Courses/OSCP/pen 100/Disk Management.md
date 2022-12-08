The most prevelant tools to interact with disks and filesystems are free, dd, du, df and mount.

The 'free' command displays information on memory.  We can use either the '-m' or '-g' option to display information in 'gb' or 'mb'.

The 'df' command (stands for 'disk free') reports on the available diskspace on each of the disks mounted on the filesystem.  The '-h' option provides information in human readable format.  

The other commands provide similar information:

* dd - is mostly used to raw copy a device file on a block level.
* du - can be used to determine the size of files and directories.  The '-hs' option is typically used to make the output human readable.
* df - and its '-T' option can be used to show the type of filesystem.

## Linux filesystems
One of the key differences between Linux and other OSs, is that in Linux we have to mount a filesystem before we can use it.  Since Linux systems have a single directory tree, if we want to insert a USB drive we would need to create an associated location somewhere in that tree.  Creating that associated location is called 'mounting'.

The 'mount' command can be used to display the currently mounted filesystems and their types.  It can also be used to mount partitions or image disk files to a mount point.

~~~ bash

mount -t ext4

# this command displays the partitions formatted as 'ext4'

# the following steps are used to mount a 'USB' drive.

sudo fdisk -l
# this is used to gather some information about the disk that has been inserted.

sudo mkdir /mnt/usb
# create a directory within standard 'mnt' directory.  This is the normal place to mount filesystems

sudo mount /dev/sdb1 /mnt/usb

# '/dev/sdb1' is the location of the inserted USB
# '/mnt/usb'  is the location to mount the USB

cd /mnt/usb
# change into the new directory to see the contents of the USB device

sudo unmount /mnt/usb
# you may need to move to a different directory to unmount














~~~

