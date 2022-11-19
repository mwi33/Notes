## Working with text files

### Looping through a text file

Create a bash file, which will be used to apply logic to the content of the relevant text file.

~~~ bash
#!/bin/bash

while read p; do

	echo "$p"

done <textfile.txt

# "while read p: do" creates a while loop to read each line of the file.
# echo "$p" is where the application logic will go.  That is to operate on each line of the text file which is contained within the variable 'p'.
# "done" exits the loop when the last line is read.

# "<textfile.txt"  is the source file that contains the data that is required

~~~

### Using sed

~~~ bash
echo "I need to try hard" | sed 's/hard/harder/'

-->I need to try harder

#  The sed application usese simple regex to changec 'hard to harder'

~~~

### Using cut
~~~ bash
echo "I hack binaries, web apps, mobile apps and just about anything else" | cut -f 2 -d ","
--> web apps

-f is the field number we are cutting 
-d is the delimter which separates the fields

# This cut function uses "," as the delimiter and this is set with the -d flag
#  This creates 3 fields: 1;"I hack binaries", 2;"web apps", and 3; "mobile apps and just about anything else"
# -f selects the second field to cut "web apps"

~~~

### Using awk

~~~ bash
echo "hello::there::world' | awk -F "::" '{print $1, $3}'

--> hello world
~~~


