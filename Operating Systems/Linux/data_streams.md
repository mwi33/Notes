# Data streams
There are three data streams created when a linux application is launced.  These are stdin, stdout and stderr.

	0 - stdin
	1 - stdout
	2 - stderr

## Redirecting data
Data from applications can be redirected to other applications or to text files.

~~~ bash

# an executable file called text_script.sh

# execute the function

./test_script.sh

# redirect the stdout to a file

./test_script.sh > output.txt

# to redirect the stderr

./test_script.sh 2> errors.txt

#  the other numbers can be used as well 0,1,2

~~~