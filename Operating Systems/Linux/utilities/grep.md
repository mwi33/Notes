# Global Regular Expression Print (grep)

grep is used to search for matches and patterns in side files and command line outputs.  It uses literal strings and [[regular expressions]].

grep can utilise the three [[data streams]] stdin, stdout and stderr 

grep can be used with other command lin applications, including:

[[cut]]
[[awk]]
[[sed]]
[[cURL]]
[[wget]]

grep syntax

~~~ bash

# searchs for the 'hello' string in the 'hello_world.txt' file

grep hello hello_world.txt

~~~

useful options (flags)

~~~ bash

# ignore case - ignores case when searching files -i

grep -i HeLlo hello_world.txt
 
# search recursively through directories.  The "." means the directory that we are in and any sub-directories -r

grep -r -i hello .

# search for whole words instead of just partial matches -w

grep -w -i hello hello_world.txt


# search for two terms (extended search) -E

grep -E -w -i "hello|world" hello_world.txt



~~~

