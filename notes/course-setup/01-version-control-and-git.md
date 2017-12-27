## Basic use of git for version control
Version control software allows developers to create a revision history of all the changes we make to a project as we work on it.  Version control lets us tag versions that we like and want to keep as snapshots. It lets us create "branches" of our code so we can try new things or develop new features without affecting the good, working code that's on the main branch.  As we'll see, it also lets us share and publish code, and gives us a neat path for distributing code to different development systems or deploying code to our production environment.  

We're going to use `git` to manage our code as we develop the projects in this course.  git's commands and language may seem complicated at first.  Understanding a few basic concepts should help things make sense.

First, some configuration would be in order.  You can look at the configuration of git by running `git config --list` at the command prompt.  Many of these configuration parameters you don't need to worry about right now, but here are a few you'll want to set up.

1. Set git up with your identity. This information will be associated with code you commit to git.  
```bash
$ git config --global user.name "Larry Bouthillier"
`$ git config --global user.email lbouthillier@fas.harvard.edu
```
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

Log into your github account, go to Settings -> SSH and PGP Keys

![github ssh keys screen][github-ssh-keys]

Click on New SSH Key and you'll see a form into which you can paste your key.  

![New ssh key in github form image][new-ssh-key-form-github]

Give your key a meaningful title to help you keep track of what machine this key was generated for.  For example, I might call mine "Larry's Mac Laptop".  

In the 'key' field, you'll paste the contents of your public key.  You can get this by going to your local .ssh directory and listing the contents of your id_rsa.pub file:

```bash
cd ~/.ssh
cat id_rsa.pub
```
You'll see something like this:
```bash
$ cd ~/.ssh
$ cat id_rsa.pub
ssh-rsa S32aB3NzaC1yc2EAAAASKDFKKSLSBAQDcTqQOkl+n0oskAWu3bZ48MnohZC2eUVuTPXpQHTQw0Qp1SzxDiY+yaTv5Rb1vYr
X06STs1PoGHY2D/JrUe9PMuxbEXpH0W1mGEavjp42oyz1Fv3sldfkdslfkdjssdZZX67ddKBeyN7RIEH348459djdee2pzBqy4k3R02
KVAqqRmLYwsqGwfMdRHjXmv+a4ZyiNy8MvZy8tta8rnLKs9pkBgtaaIfGHtt7/VHJ7jUZYz0kmEJ3sWrVItDlzFn7OlnIym3+gampJd
de5TWS7M1UbbGVjHk+gR68fx5U0IrNPvUnd0WHMbPXd2whIVTTulaomgwfhgWp4uTh/WqJv+j lbouthillier@fas.harvard.edu
$
```
Copy the entire text starting with `ssh-rsa` and ending with your email address and paste it into the github form, and click the Add SSH Key button.

#### Test our connection to github

You can test your connection with this command:

`ssh -T git@github.com`

The first time you do this, you may see a message like this:

```bash
The authenticity of host 'github.com (207.97.227.239)' can't be established.
# RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
# Are you sure you want to continue connecting (yes/no)?
```

Type *yes* and hit enter.  If all went well, you should see a message like this:

```bash
$ ssh -T git@github.com
Hi lbouthillier! You've successfully authenticated, but GitHub does not provide shell access.
$
```

If you don't see this message, have a look at the [Github SSH connection troubleshooting page](https://help.github.com/articles/error-permission-denied-publickey/), and reach out on the course Piazza forum for assistance.

### Using git and github

This is not a course focused on development operations or management practices. We're going to
cover the use of git and github just enough to cover our very basic needs for this course.  

#### Create a Repository

The first thing we'll do with our new git and github setup is to create a Repository for our first project.  We'll explain exactly what a Repository is and what it means in a moment, but for now, follow the steps to set up a new one on github.   

From [the github homepage](https://github.com/), click on New Repository.

![new-repository button in github screenshot][new-repository-github]

Use the settings shown below to create your repository.

![github-new-repository][New repo settings: provide a repository name, set as public (unless you have a paid subscription),initialize with a README, no gitignore, no license] [github-new-repository]

#### Clone the Repository Locally

Now we'll clone this repository to our local computer.  Each repository on github has an SSH address, found as shown here:

![SSH address found under Clone of Download, a field called 'Clone this repository at'][github-get-ssh-url]

Now, from the command prompt on your computer, navigate to the directory where you'd like to work on your project.  You may want to create a directory called cscie31 (or something like that) for your course projects.  

We're going to fetch the repository from github, which will create a folder in your local directory and fill it with your project files.  Type the following command, using the SSH address you copied from github.  

`git clone git@github.com:your-github-username/cscie31-welcome.git`

If all went well, you should see something like this:

```bash
$ git clone git@github.com:LPBSandbox/cscie31-welcome.git
Cloning into 'cscie31-welcome'...
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.
$
```
Look in your cscie31 folder and you'll see the project folder.

```bash
$ ls
cscie31-welcome
$ ls cscie31-welcome/
README.md
$
```

Let's modify the README.md file, and then update the github repository.

Use nano to edit the file:

`nano README.md`

Make a change to the file - perhaps add a line that says "I changed this!", or anything else, and save it using `crtl-X`,to exit, then `Y` to save.

![screenshot of nano screen][nano-change-readme]

#### Track Our Changes

We still need to do a few steps to get this tracked by git. At its simplest, git has two areas for your code, with an important in-between third state:

1. The *working directory* where you create and modify your code
2. The .git directory *repository* where changes that you're finished with, or that you want to preserve a snapshot of, are *committed*.  
3. There's an important in-between state for your files - when you want to tag new or modified files as ones you'll be committing, you *add them to the index*, typically referred to as *staging* the files.  Our optional reading reference refers to this as "the loading dock where you get to determine what changes get shipped away".

Once the files are in your repository, you can push them to remote locations, such as github.  We'll walk through those steps next. Meanwhle, these optional but recommended readings may help build your understanding of git.

#####Recommended Reading:
+ [Nick Quaranto's The Staging Area](http://gitready.com/beginner/2009/01/18/the-staging-area.html), from the very helpful [gitready.com](gitready.com)  
+ Git-scm's [Getting Started - git Basics](https://git-scm.com/book/en/v2/Getting-Started-Git-Basics)
+ A very basic [Git walkthrough via simulation](https://try.github.io/levels/1/challenges/1), from github

#### Add files and commit to git
Let's see what the status is of our git repository, or 'repo'. Type  `git status`

```bash
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

It's telling us that we have a changed file, but it's not "staged".  "Staging" a file is simply marking it as one we'll be tracking and committing.

Tell git to start tracking this file by adding it to the "staging area".  

`git add .   // the dot means "all new and changed files`

Then do `git status`.  You should see something like this:

```bash
$ git add .
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   README.md

$
```

I think we're ready to commit these changes. Each commit should have a comment that reminds you what you changed or why you did it. For example, you may mention what feature or bug you were working on. The `-m` flag indicates your comment.

```bash
$ git commit -m "Changed the README file per lesson instructions"
[master 06a23e7] Changed the README file per lesson instructions
 1 file changed, 2 insertions(+), 1 deletion(-)
$
```

Finally, we're going to push our repository up to our github account.  We'll use `git push` which will take two arguments:
1) the remote repository to push to.  When we cloned our code from github, our remote repository was named *origin* on our behalf.   
2) which branch of our code to push.  We haven't talked about branches, and we won't be requiring them for work in this course.  By default, the main branch of our code is called *master*.

So, the command we'll use to push our code to github will be:

`$ git push origin master`

You should see something like this:

```bash
$ git push origin master
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 334 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To github.com:LPBSandbox/cscie31-welcome.git
   225c177..06a23e7  master -> master
$
```

Take a look on github using your browser and check to see that your changes made it.   

#### A Server-side Node Program

Let's make a real Node program you can deploy to your Digital Ocean Server in the next step.  In the example we did last week, we wrote a small program that made an HTTP GET request on a url and outputs the result to the console.  

```Javascript
var h=require('http');
h.get('http://www.google.com/',
  function(r){
    r.setEncoding('utf8')  
    r.on('data', function(d){
      console.log(d);
    });
});
```

This time, we'll use the same HTTP capability to respond to a GET request, essentially making a little Web server.  Using the editor of your choice, create a file called stringserver.js in your cscie31-welcome directory, and paste in the following code and save it.

```Javascript
var http = require('http');
var server = http.createServer(function(req, res) {
    res.writeHead(200);
    res.write("Hello World");
    res.end();
});
server.listen(8080);
console.log("Listening on http://127.0.0.1:8080/");
```
Now from the command-line, we're going to run this program. Navigate to the directory where this file lives, and type `node stringserver`. Note that we don't need to use the .js filename extension here. Direct your browser to http://localhost:8080/.  You'll see the value of the string being written to the `response` object.  To stop your program, press `crtl-C`.

Congratulations on your first Node program!   











[sshkey-diagram]: img/digital-ocean-ssh-keys-description.png
[github-ssh-keys]: img/github-ssh-keys.png
[new-ssh-key-form-github]: img/new-ssh-key-form-github.png
[new-repository-github]: img/new-repository-github.png
[github-new-repository]: img/github-new-repository.png
[github-get-ssh-url]:img/github-get-ssh-url.png
[nano-change-readme]:img/nano-change-readme.png
