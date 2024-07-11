# Overview
The zsh terminal keeps a file that stores the commands you've typed before.  This file is called the history file.  At times this file can become damaged or corrupt, which in turn causes a variety of errors when the terminal is started.

## Fix
To fix the corrupt file we create a new one and move the commands from the corrupt file to a new one.

~~~ bash
# rename the corrupt file to .zsh_history_bad

mv .zsh_history .zsh_history_bad

# use the strings command to move the commands from the corrupt file to a new .zsh_history file

strings .zsh_history_bad > .zsh_history

# instruct the zsh terminal to use the new .zsh_history file

fc -R .zsh_history

# delete the old .zsh_history file

rm .zsh_history_bad

~~~