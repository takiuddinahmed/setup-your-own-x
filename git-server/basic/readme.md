# Setup Your Own Git Server (Basic)

Here we will setup git server in AWS EC2 hosted Ubuntu server

## Step 1 - Installation

At first we will install git in our machine

```bash
sudo apt update && sudo apt install git
```

## Step 2 - Add User

Now we will create a user for git access

```bash
sudo useradd -r -m -U -d /home/git -s /bin/bash git
```

Here,

- `-r` indicates the user will be a system user
- `-m` indicates user will create a home directory
- `-d` indicates the home directory. Here `/home/git` will be home directory of the user
- `-s` indicates the shell. Here bash shell is used
- `git` is the the username

Then, we will login as `git` user

```bash
sudo su - git
```

## Step 3 - Setup SSH with authorization

We will create `.ssh` folder with permission to store authorized keys

```bash
mkdir -p -m 0700 ~/.ssh
```

Here,

- `-p` indicates that the folder will be created if the folder does not exist
- `-m` indicates to setup permission of the folder

Then, we will create a file to store authorized keys

```
touch ~/.ssh/authorized_keys && chmod 0600 ~/.ssh/authorized_keys
```

## Step 4 - Create git repo

Now we will create one or more git repository in the server. This repository will be shared for all

```bash
git init --bare ~/projectname.git
```

## Step 5 - Configure local system

We will create a new SSH key pair on our local system.

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@domain.com"
```

If there already ssh key pair exists then no need to create.

Now, we will display the key pair

```
cat ~/.ssh/id_rsa.pub
```

we will copy the output value

## Step 6 - Add auth in git server

We will go to the git server and open the authorized_keys file using a text editor

```bash
nano ~/.ssh/authorized_keys
```

Then we will paste the copied public key in one single line

## Step 7 - Setup Git project

We will install git in your local machine if not installed.

We will create a project

We will initialize a git repository

```bash
git init
```

We will add git remote

```bash
git remote add origin git@git_server_ip:projectname.git
```

We will add a file

```bash
touch new_file
```

We will add changes to the staging area

```bash
git add .
```

We will commit the changes

```bash
git commit -m "message"
```

Push the changes to the remote repository

```bash
git push -u origin master
```
