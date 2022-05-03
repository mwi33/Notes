# Workflow

1.  Generate new ssh keypair
2.  Store keypair
3.  Copy public key to remote server
4.  Authenticate with ssh keys

## Generate new ssh keys

~~~ bash
ssh-keygen -t rsa -b 4096 -C mwi33@email.com
# -t is the type of algorithm (rsa)
# -b is how many bytes the keys should be
# -C is a comment
~~~

During the process of generating keys, a prompt to select the storage location is provided.  The default location is /home/user/.ssh/.

A prompt to provide a passphrase is also provided.

## Copy public key to remote server

There are two ways to copy keys to the remote server.  Firstly, using the standard 'scp' command.  Once copied, this key needs to be added to the authorized_keys file ont he server.

A easier method is to use the 'ssh-copy-id command.  This command copies the public key to the remote server add it to eh authorized_keys file.

~~~ bash
ssh-copy_id -i <path-to-id_rsa.pub> user@targetIP

# -i is the key file
~~~

## Authenticating

Using the ssh command will now use the keys rather than a password.
