
- Linux is a kernel not an operating system;
- Its primary function is to manage hardware;
- The programming layer also provides an abstraction layer;
- The kernel exports data about detected hardware through the /proc/ and /sys/ virtual file systems;
- Applications access devices by way of files created in the /dev/.
- Specific files represent disk drives (/dev/sda)
- There are two types of device files, block and character.  Block has the characteristics of a block of data and character has the characteristics of a flow of characters.  With the block, you can navigate to a particular point of the data.  With character you can read and write data but not move to a given point.

``` bash

# using ls -l you can see the type of device file

ls -l

brw
crw

```
## Unifying file system

UNIX like systems merge all file stores into a single hierarchy which allows users and applications to access data by knowing its location within that hierarchy.  The starting point of this hierarchy is root '/'.  The subdirectory of root is home, which is shown as '/home/'.

Linux systems contain only one hierarchy and it can integrate data from several disks.  One of these disks becomes root and the others are mounted on directories in the hierarchy.  The 'mount' command is used to mount additional disk within a direcroty in this hierarchy.  That data is then available from within that directory.

There are many differenty formats for file systems (ext2, ext3, and ext4).  Windows uses VFAT.  Linux supports mounting VFAT file system under kali.  The process of preparing file systems for mounting is called formatting.  This means that the users home drive can be mounted on a separate disk and will be available when mounted.

Commands line 'mkfs' (make file system), undertake the formatting process.  This commands requires a parameter, which is the device file which represents the partion to be formatted.  This operation is destructive and should only be used once as it wipes the content from the drive.

## Environment variables

Environment variables allow storage of global settings for the shell or various other programs.  

## Filesystem Hierarchy Standard (FHS)

Kali is consistent with the FHS, allowing users of other Linux distributions to easily find their way.  The FHS defines the purpose of each directory.

## Useful commands

~~~ bash

echo 'kali is the best' > kali.txt
cat kali.txt
kali is the best

echo "kali is awesome' >> kali.txt
cat kali.txt
kali is the best
kali is awesome

find /etc -name hosts

fit /etc -name "hosts*"


~~~
