## Basic use of git for version control
Version control software allows developers to create a revision history of all the changes we make to a project as we work on it.  Version control lets us tag versions that we like and want to keep as snapshots. It lets us create "branches" of our code so we can try new things or develop new features without affecting the good, working code that's on the main branch.  As we'll see, it also lets us share and publish code, and gives us a neat path for distributing code to different development systems or deploying code to our production environment.  

We're going to use `git` to manage our code as we develop the projects in this course.  git's commands and language may seem complicated at first.  Understanding a few basic concepts should help things make sense.

First, some configuration would be in order.  You can look at the configuration of git by running `git config --list` at the command prompt.  Many of these configuration parameters you don't need to worry about right now, but here are a few you'll want to set up.

1. Set git up with your identity. This information will be associated with code you commit to git.  
`$ git config --global user.name "Larry Bouthillier"``
`$ git config --global user.email lbouthillier@fas.harvard.edu`
2. Make it easier to read with color output:
`$ git config --global color.ui true`
3. Tell git to ignore filemode changes:
`$ git config --global core.filemode false`
4. Set up the default command-line text editor to use with git. We choose nano below, but if you have a different favorite you can use that.
`$ git config --global core.editor nano`

## Sharing and Publishing Code on Github
Code in git lives in repositories, which represent the code associated with a project. One such repository will live on your own computer, managed by git and stored in the folder where you're working on your project.  You can also push code to other, remote repositories where it can be published and shared.  We'll be using *[github](https://github.com)* as this remote repository in this course.  Here are the steps to setting up a free github account for your work.

**NOTE:** If you already have github account, you're welcome to use that one for your coursework. If you have a github account, but don't have SSH keys set up, skip to that part of the directions below.

### Setting up a github account and SSH keys
In this section, we're going to do the following:
1. Create a github account
2. Create SSH keys on our local computer
3. Configure our github account with our SSH public key
4. Test our connection to github

#### Create a github account
This one's easy. Go to github and sign up for a free account.

#### Create SSH keys on your local computer
SSH is a secure communications protocol we'll be using to connect to github from your local git repository.  Rather than using passwords to authenticate, we'll generate a unique pair of keys - one public key that you'll share with github, and one associated private key that lives on your computer.  As it happens, we're going to be using the same process to connect to Digital Ocean, our server host for this course.

Optional Reading: [Digital Ocean SSH Essentials: Working with SSH Servers, Clients, and Keys](https://www.digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys) (SSH Overview section)

![SSH Key Diagram][sshkey-diagram] (Source: Digital Ocean)

The following directions are drawn from [Digital Ocean SSH Essentials: Working with SSH Servers, Clients, and Keys](https://www.digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys#generating-an-ssh-key-pair)

To generate an RSA key pair on your local computer, type:
`ssh-keygen -t rsa -C "your-email-goes-here"`

```
Generating public/private rsa key pair.
Enter file in which to save the key (/home/demo/.ssh/id_rsa):```


This prompt allows you to choose the location to store your RSA private key. Press ENTER to leave this as the default, which will store them in the `.ssh` hidden directory in your user's home directory. Leaving the default location selected will allow your SSH client to find the keys automatically.

```
Enter passphrase (empty for no passphrase):
Enter same passphrase again:```


The next prompt allows you to enter a passphrase of an arbitrary length to secure your private key. By default, you will have to enter any passphrase you set here every time you use the private key, as an additional security measure. Feel free to press ENTER to leave this blank if you do not want a passphrase. Keep in mind though that this will allow anyone who gains control of your private key to login to your servers.

[NOTE: if you use a passphrase here, you'll have to enter it every time you do an operation using ssh.  For a production server, this would be advisable. For development work and our course purposes, it can be more convenient to leave the passphrase blank.]

If you choose to enter a passphrase, nothing will be displayed as you type. This is a security precaution.

```
Your identification has been saved in /root/.ssh/id_rsa.
Your public key has been saved in /root/.ssh/id_rsa.pub.
The key fingerprint is:
8c:e9:7c:fa:bf:c4:e5:9c:c9:b8:60:1f:fe:1c:d3:8a root@here
The key's randomart image is:
+--[ RSA 2048]----+
|                 |
|                 |
|                 |
|       +         |
|      o S   .    |
|     o   . * +   |
|      o + = O .  |
|       + = = +   |
|      ....Eo+    |
+-----------------+


This procedure has generated an RSA SSH key pair, located in the .ssh hidden directory within your user's home directory. These files are:
  ~/.ssh/id_rsa: The private key. DO NOT SHARE THIS FILE!
  ~/.ssh/id_rsa.pub: The associated public key. This can be shared freely without consequence.```

#### Configure our github account with our SSH public key




[sshkey-diagram]: img/digital-ocean-ssh-keys-description.png
