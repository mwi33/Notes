### cat
cat is used to view the contents of one or more files in the terminal without opening them.  

Syntax
~~~ bash
cat <file path> # displays the contents of the file in the terminal
cat -n <file patth> # includes line numbers
cat >newfile.txt # creates a new file and provides an interface to add content.  Use ctrl-d to exit the editor 

####

# transfer contents from one file to another

cat file1.txt > file2.txt # if file2 doesn't exist, it is created.

cat file1.txt file2.txt > file3.txt

####

# display in backwards order

tac file1.txt

####

# apend data to the end of an existing file

cat file1.txt >> file2.txt

cat >> file1.txt

####

# process large files

cat file1.txt | more # shows data one page at a time
~~~