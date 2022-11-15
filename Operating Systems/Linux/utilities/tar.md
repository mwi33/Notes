Extrtact data from tar.gz file

~~~ bash

# -x is to extract the file
# -f should proceed the file that is to be unzipped

tar -xf filename.txt.tar.gz


~~~

Comporess data with the tar command

~~~ bash

# -c is to create an archive
# -z is to compress the archive with gzip
# -v Display progress in the terminal while creating the archive, also known as 'verbose' mode.  -v is always optional.
# -f Allows you to specifiy the filename of the archive

tar -czvf name-of-compressed-file.tar.gz /path/to/directory-or-file

~~~
