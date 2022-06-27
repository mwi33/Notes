# Docker

## Components

### Dockerfile
A dockerfile specifies how an image should be built.

### Image
Contains all the code but doesn't do anything yet.

### Container
A container is a running image.

## Example

1. Create a folder to hold the dockerfile and other related files.
2. Create a dockerfile which contains the following:

~~~ bash
# A dockerfile must always start by importing the base image.
# We use the keyword 'FROM' to do this.
# In this example, we want to import the python image.
# So we write 'python' for the image and 'latest' for the version

FROM python:latest

# In order to lauch our python code, we must import it into our image.
# We use the keyword 'copy' to do that.
# The first [arameter 'main.py' is the name of the file om the host.
# The second parameter '/' is the path to where to put the file on the image.
# Here we put the file at the image root folder.

COPY main.py /

# We need to define the command to launch when we are going to run the image.
# We use the keyword 'CMD' to do that.
# The following command will execute "python ./main.py".

CMD [ "python", "./main.py" ]
~~~

3.  Create the main.py file, which should contain the code that will run.

~~~ bash
#!/usr/bin/env python3

print("Docker is magic!")
~~~

4.  Build the docker image.

~~~ bash

# This command should be run from within the same directory as the docker file and other dependencies.

sudo docker build -t <name of image>

~~~

5.  Run the docker container.

~~~ bash

sudo docker run <name of image>

~~~