# Git and Github
## Git
### Overview
git is a source code management system.  It is used  to track changes to files and manage planned changes.  It includes the capacity to collaborate with other developers using a combination of both local and remote repositories.

### Installing git
Git should be installed using the relevant package manager (apt for Debian distributions).

~~~ bash
# installs git using the apt package manager
sudo apt install git

# returns the installed version of git
git version
~~~

Once installed with your pacakage manager, the application will be updated through the 'apt update' and 'apt upgrade'.

### Local repositories
Local repositories are essentially just a folder that containes files that will be managed using git.  Local repositories can be created in several ways.  Generally, this is either by cloning a remote repository from github (or other remote repository), or by creating content locally and then adding a remote repository afterwards.

Once a local repository has been established (cloning or initiating), git commands can be used to manage source code (text files).

### Git workflow
At the simplest level, git manages changes made at a local level, often by several developers.  
#### Git states
A file can be in one of several states (committed, modified/untracked, staged).  Git commands are used to change the state of a file.
1.  'Untracked' means that the file is new to the git projects;
2.  'Modified' means that the file has been seen, but has been changed so it is not ready to be snapshotted yet;
3.  'Staged' means that a file has been added to the staging area (logical) and can be snapshotted by git and store its current state in the git repository.  

#### Git commands
##### Git add
Within the working directory (folder), files, either new or modified need to be added to the staging area so that then can be snapshotted when needed.  The 'git -add' command adds new and modified files to the staging area.

~~~ bash

# git add syntax
# git add <path>

git add readme.md

~~~

##### Git commit
Once files have been added to the staging area, which is essnetially a catalogue of files that are to be tracked, they can be committed to the 'local repository'.  Committing files takes a snapshot of the files in the 'staging area' and adds them to the 'local repository'.
~~~ bash

# commit files that have been added to the staging area, which expliclity marks them for tracking.

# a git commit takes a snaopshot of these files and adds them to the 'staging area'.

# Syntax

# --all : includes all files that have been added to the 'staging area'
# -m : a mandatory message to describe the change being committed

git commit --all -m 'This is the message'

~~~

##### Git push
After changes are committed to the local repository (from the staging area), they are then integrated with the code of other developers in a aggregate, remote repository.  These remote instances include GitHub and BitBucket.

~~~ bash

# pushes files to the remote repository

# this integrates local code with that of other develoeprs in a remote repository.

git push

~~~
##### Git status
Git status provides the status of the working tree.  Essentially, changes that have either not been added or committed.

~~~ bash

git status

~~~

### Git files
#### readme.md
#### .gitignore

## Github
### Remote repositories

### Setup
Once git is installed, it needs to be configured so that it can manage text files and integrate with remote repositories like github. 

#### Github configuration

~~~ bash
# these commands are used to configure the user details on a local machine.
# the username and email are those associated with your github account
git config --global user.name "username"
git config --global user.email "email"

~~~

google cheat sheet

https://duckduckgo.com/?q=git+commands&t=newext&atb=v243-1&ia=cheatsheet&iax=1

git init [project name]

git clone[url]

git status

git config --global user.name "[username]"
git config --global user.email. "[email]"

git remote add [remote name] [url]

git add [file]
git commit -m "[message]"
git push

git pull
