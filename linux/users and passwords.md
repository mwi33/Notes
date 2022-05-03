# List local users
~~~ bash

# list local users

cat /etc/passwd

~~~

# whoami

~~~ bash

# list the logged in user

whoami

~~~

# Change root password
~~~ bash

# change password

passwd

# you will be prompted  to enter your existing passward and your new password twice.

~~~

# Create a new user
~~~ bash

# create a new user

sudo adduser username

# you will be promoted to add a password, full name and some additional information which can be skipped.

# a home directory will be created for the new user

~~~

# Change user
~~~ bash

# change users

su username

# you will be promoted for a password

~~~