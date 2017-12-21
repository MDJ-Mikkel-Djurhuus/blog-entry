setup/install jenkins

Make a freestyle project

![create a new project](./jenkins-freestyle-project.PNG)

Setup source code management (link to git and chose branch)

![setup git](./jenkins-source-code-management.PNG)

Build script (workspace is now the chosen git)

![build script](./jenkins-docker-password.PNG)

![build script](./jenkins-docker-password-enable.PNG)

![build script](./jenkins-build.PNG)

to be able to ssh into our production server, we need to create a public

deployment script
```
#!/bin/bash
IMAGE_NAME=$1
SERVICE_NAME=$2
BUILD_NUMBER=$3

docker pull mikkeldjurhuus/${IMAGE_NAME}:${BUILD_NUMBER}
docker-compose up -d --no-deps --build ${SERVICE_NAME}
docker image prune -a
```

### Generate a Key Pair
To generate a new key pair, ssh into your jenkins server and enter the following command in the terminal:
```
ssh-keygen
```
Assuming your local user is called "localuser", you will see output that looks like the following:
```
ssh-keygen output
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/localuser/.ssh/id_rsa):
```
Hit return to accept this file name and path (or enter a new name).

This generates a private key, id_rsa, and a public key, id_rsa.pub, in the .ssh directory of the localuser's home directory. Remember that the private key should not be shared with anyone who should not have access to your servers!

### Copy the Public Key
After generating an SSH key pair, you will want to copy your public key to your production server.

Assuming you generated an SSH key pair using the previous step, use the following command at the terminal of your jenkins server to print your public key (id_rsa.pub):
```
cat ~/.ssh/id_rsa.pub
```
This should print your public SSH key, which should look something like the following:
```
id_rsa.pub contents
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDBGTO0tsVejssuaYR5R3Y/i73SppJAhme1dH7W2c47d4gOqB4izP0+fRLfvbz/tnXFz4iOP/H6eCV05hqUhF+KYRxt9Y8tVMrpDZR2l75o6+xSbUOMu6xN+uVF0T9XzKcxmzTmnV7Na5up3QM3DoSRYX/EP3utr2+zAqpJIfKPLdA74w7g56oYWI9blpnpzxkEd3edVJOivUkpZ4JoenWManvIaSdMTJXMy3MtlQhva+j9CgguyVbUkdzK9KKEuah+pFZvaugtebsU+bllPTB0nlXGIJk98Ie9ZtxuY3nCKneB+KjKiXrAvXUPCI9mWkYS/1rggpFmu3HbXBnWSUdf <user>@<machine>
```
Select the public key, and copy it to your clipboard.

To enable the use of SSH key to authenticate as the new remote user, you must add the public key to a special file in the user's home directory.

On the server, as the root user, enter the following command to temporarily switch to the new user (substitute your own user name):
```
su - sammy
```
Now you will be in your new user's home directory.

Create a new directory called .ssh and restrict its permissions with the following commands:
```
mkdir ~/.ssh
chmod 700 ~/.ssh
```
Now open a file in .ssh called authorized_keys with a text editor. We will use nano to edit the file:
```
nano ~/.ssh/authorized_keys
```
Now insert your public key (which should be in your clipboard) by pasting it into the editor.

Hit CTRL-x to exit the file, then y to save the changes that you made, then ENTER to confirm the file name.

Now restrict the permissions of the authorized_keys file with this command:
```
chmod 600 ~/.ssh/authorized_keys
```
Now your public key is installed, and you can use SSH keys to log in as your user.
