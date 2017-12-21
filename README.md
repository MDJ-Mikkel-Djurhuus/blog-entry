## Continuous delivery, From Study To Success In 1 Day.

# Abstract

We all know the feeling of pushing new development code unto the production environment. Hoping, wishing, it'll work and there isn't some unforseen circumstance which forces us into panic mode, because now the entire production environment is flashing red and nothing is working. 

In the situation of a production faliure, getting the system back on track is essential. which is why we want to setup a continuous delivery environment, that can speed up the release of a hotfix. Specifically we'll look at using Jenkins, and how it can be used together with Docker and Git, to lower the "mean time to recovery".

With a continuous deployment environment up and running, everytime a developer pushes code to the specified Git branch, Jenkins will build and deploy the updated code to the desired environment, preferably release. Ensuring every consumer is always on the newest update and benefits from new features as soon as possible.

# Jenkins / Git / Docker - Just how easy it is to setup a CD environment

After installing jenkins create a new Freestyle project

![create a new project](./jenkins-freestyle-project.PNG)

## Connecting Jenkins to Git

Go to the Source Code Management section and specify the git repository and branch we want to use. 

![setup git](./jenkins-source-code-management.PNG)

This will set the workspace of our jenkins project to use the specified git repository, but we still haven't told git about our jenkins server. To let jenkins react to github changes we need to configure a webhook.

This is done logging into our github repository and navigate to settings => integrations & services. 

Here we add a new service by searching for "jenkins" and choosing the "Jenkins (Git plugin)".

![setup git](./jenkins-git.PNG)
![setup git](./jenkins-githook.PNG)

## Building and deploying have never been easier

Now we need specify what should happen whenever git recieves a new commit to the release branch.

Using docker to containerize our applications, makes for a very simple the build step. All the build script needs to do is building the docker image and push it to our dockerhub account.

As we dont want people to see our docker password we create a secret text, which we then enable in the Build Environment

Out of our project, Navigate to the Global credentials section and click on "Add Credentials"
![build script](./jenkins-docker-password.PNG)
In our project navigate to the Build Environment section and specify our secret text
![build script](./jenkins-docker-password-enable.PNG)
We can now use `${DOCKER_PWD}` in our scripts

Go to the build section and add two new build steps, one for building and one for deploying.

![build script](./jenkins-build.PNG)

Steps in our build script:
- Build the docker image (workspace is automaticly set to use the github repository)
- Login to docker hub (using our secret)
- Push our image to docker hub (using jenkins environment variable BUILD_NUMBER to specify the image version )

If jenkins succesfully builds and deploys the docker image, it will continue and run our deployment script, which specifies the deployment to our production server.

Deployment steps:
- Pull the newly build image
- Rebuild the service using our image and restart it.
- Cleanup old images

Contents of the bash file "./deploy.sh":
```
#!/bin/bash
IMAGE_NAME=$1
SERVICE_NAME=$2

docker pull mikkeldjurhuus/${IMAGE_NAME}:latest
docker-compose up -d --no-deps --build ${SERVICE_NAME}
docker image prune -a
```

THATS IT!? A commit to the relase branch will now trigger jenkins to build and deploy our docker application.

## Did we just make a Remote deployment!?
In the previous steps we log into our production server using SSH and execute a deployment script:  `ssh builder@146.185.141.49 "./deploy.sh"`. SSH, or secure shell, is an encrypted protocol used to administer and communicate with servers. While there are a few different ways of logging into an SSH server, in this guide, we'll focus on setting up SSH keys.
### Generate a Key Pair
To generate a new key pair, we login on our jenkins server and enter the following command in the terminal:
```
ssh-keygen
```
As we are logged into a user called builder, the output looks like the following:
```
ssh-keygen output
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/builder/.ssh/id_rsa):
```
Hit return to accept this file name and path (or enter a new name).

This generates a private key, id_rsa, and a public key, id_rsa.pub, in the .ssh directory of the localuser (builder)'s  home directory. Remember that the private key should not be shared with anyone who should not have access to your servers!

### Copy the Public Key
After generating the SSH key pair, we need to copy the public key to our production server.

follwing the previous step, we can use the following command to print our public key (id_rsa.pub):
```
cat ~/.ssh/id_rsa.pub
```
This should print our public SSH key, which looks something like the following:
```
id_rsa.pub contents
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDBGTO0tsVejssuaYR5R3Y/i73SppJAhme1dH7W2c47d4gOqB4izP0+fRLfvbz/tnXFz4iOP/H6eCV05hqUhF+KYRxt9Y8tVMrpDZR2l75o6+xSbUOMu6xN+uVF0T9XzKcxmzTmnV7Na5up3QM3DoSRYX/EP3utr2+zAqpJIfKPLdA74w7g56oYWI9blpnpzxkEd3edVJOivUkpZ4JoenWManvIaSdMTJXMy3MtlQhva+j9CgguyVbUkdzK9KKEuah+pFZvaugtebsU+bllPTB0nlXGIJk98Ie9ZtxuY3nCKneB+KjKiXrAvXUPCI9mWkYS/1rggpFmu3HbXBnWSUdf builder@jenkins-server
```
Select the public key, and copy it to your clipboard.

To enable the use of our SSH key to authenticate our jenkins server, we must add the public key to a file called authorized_keys inside a folder called .ssh at the home directory for our build user

On the server, as the root user, we enter the following command to switch to our build user (substitute your own user name):
```
su - builder
```
This will take us to the home directory for the user "builder".

Now we create the directory called .ssh and restrict its permissions with the following commands:
```
mkdir ~/.ssh
chmod 700 ~/.ssh
```
We will use nano to edit the authorized_keys file: (if the file doesn't exist it will automaticly be created)
```
nano ~/.ssh/authorized_keys
```
Now we insert the public key (which we copied earlier) by pasting it into the editor.

Hit CTRL-x to exit the file, then y to save the changes that you made, then ENTER to confirm the file name.

Now restrict the permissions of the authorized_keys file with this command:
```
chmod 600 ~/.ssh/authorized_keys
```
Now we have a public key installed, which means we now can SSH into our production server, from our jenkins server.

# What now?

Now you've gained insigt in how to setup the CD workflow. But there's so much more to learn, use and master. This can easily be extended with a continuous integration part for example. 

By implementing a continuous integration stage to the workflow, we'd have a proper quality check for what code is allowed to be merged and pushed unto the release. Without that check, we're left in the hands of our developers. Which is actually what we're trying to avoid. Letting jenkins handle merging of  branches and running tests. However, everything thing starts with step 1.

Besides Jenkins there are many other tools which can help you automate your development workflow. We have chosen to focus on Jenkins since it's what we used. There are alternatives to do the same thing, and other tools to handle different automation stages of development.

# References
https://github.com/datsoftlyngby/soft2017fall-lsd-teaching-material/blob/master/lecture_notes/05-Continuous%20Integration%20and%20Delivery.ipynb

https://en.wikipedia.org/wiki/Mean_time_to_recovery

https://en.wikipedia.org/wiki/DevOps

http://skillslane.com/ultimate-list-devops-tools/ (List of tools that can be used in a devops workflow)

https://en.wikipedia.org/wiki/Continuous_delivery

https://en.wikipedia.org/wiki/Continuous_integration

https://jenkins-ci.org/

https://www.docker.com/

https://git-scm.com/

https://github.com/
