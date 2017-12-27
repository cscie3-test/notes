## Setting Up Your Digital Ocean server
In this course, you'll be publishing your homework projects to github, and deploying them to Digital Ocean (DO), where you and the teaching staff can see the code execute.  

Digital Ocean isn't totally free.  The running costs for your DO server for the duration of this course will come to about $5 per month.    

We're going to do the following steps to get set up on DO:
1. Set up an account on DO
2. Set up our SSH key for logging in
3. Provision an instance of a Node/Ubuntu server
4. Log in to our DO server
5. Set up SSH keys between the server and github
6. Clone our github repository (or repo) to DO and run some code   

### Set up an account on DO
Go to [Digital Ocean](https://digitalocean.com) and register for an account.  During this process, it will ask you for a payment method.  To be clear, there are no charges for registering an account on Digital Ocean.  You do pay for the individual server instance you'll create in the following steps, though.

### Set up our SSH key for logging in
Once you're logged into DO, go to your account menu at the top-right of the screen, select Settings, then Security.

![DO settings menu][DO-settings-menu]

Select Add SSH Key.  We'll use the same SSH key you generated for github.  From the command-line, navigate to your `~/.ssh` directory (or `%home%/.ssh` on windows) and `cat id_rsa.pub`   Copy the key and paste it into the Digital Ocean SSH key form.  Be sure to give it a useful name that describes which computer this key goes to.  Mine might be "Larry's Development Laptop", but you can call it anything you like.  

### Provision an instance of a Node/Ubuntu server

For this class, we're going to provision a new Droplet, DO's terminology for a server instance.  From the Digital Ocean Droplets page, Choose Create -> Droplets.  On the next screen, under *Choose An Image* select *One-click apps*, and then make the following selections (shown below):

+ Choose an image:
  + One-click apps
  + Select the image with the highest version of NodeJS 6.x or NodeJS 8.x (don't use 7.x or 9.x if that's available)
+ Choose a size:
  + The $5/month size is sufficient for this class
+ Choose a datacenter region:
  + You may wish to choose a region geographically close to you
+ Add Your SSH Keys
  + Select the SSH key you set up in the previous step
+ Choose a Hostname
  + Name your host as you wish, subject to the naming rules noted on the page
+ Click Create

![new D.O. Droplets selections][DO-droplets-new]

### Log in to our DO server

Take note of the IP address of your new droplet.

![D.O. droplet ip address][DO-droplet-ip-address]

Then, from the command-line, SSH to your new server by doing this:

`ssh root@[your IP address here]`

You should see something like this:

```bash
$ ssh root@104.236.220.103
Welcome to Ubuntu 16.04.2 LTS (GNU/Linux 4.4.0-78-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

65 packages can be updated.
0 updates are security updates.


*** System restart required ***
-------------------------------------------------------------------------------
Thank you for using DigitalOcean's NodeJS Application

The "ufw" firewall is enabled. All ports except for 22, 80, and 443 are BLOCKED

-------------------------------------------------------------------------------
To delete this message of the day: rm -rf /etc/update-motd.d/99-one-click
root@cscie31:~# ```

Now we're logged in to our own server!  

### Set up SSH keys between the server and github

Just as we set up an ssh keypair between our local computer and github, we're going to do the same between this Droplet and github. This will allow us to pull our code down from github to our server, where we can run it and make our applications available to the world.

The steps are the same as we did before. While still logged into our Droplet, type

 `ssh-keygen -t rsa -C "your-email-address-here"`

Accept the default for the file in which to save the key (press enter), and enter a passphrase if you like.  For purposes of this course, it's easier if you don't use a passphrase.   When you're done, you'll have a `~/.ssh` directory that contains two files: `id_rsa` and `id_rsa.pub`.

From the .ssh directory, run `cat id_rsa.pub` , copy the contents of the file, and add these as a new ssh key in [github's SSH settings](https://github.com/settings/keys).

Test your connection from the droplet:

  `ssh -T git@github.com`

If all went well, you should see a message like this:

`$ Hi lbouthillier! You've successfully authenticated, but GitHub does not provide shell access.`

### Clone our github repository (or repo) to DO and run some code

Last step!  We're going to pull our code down from github and run it on our server.  On your Droplet command-line, clone your repository from github:

```bash
$ git clone git@github.com:your-github-username/cscie31-welcome.git
root@cscie31:~# git clone git@github.com:LPBSandbox/cscie31-welcome.git
Cloning into 'cscie31-welcome'...
remote: Counting objects: 9, done.
remote: Compressing objects: 100% (6/6), done.
remote: Total 9 (delta 0), reused 6 (delta 0), pack-reused 0
Receiving objects: 100% (9/9), done.
Checking connectivity... done.
root@cscie31:~#
```

Now, navigate to your `cscie31-welcome` directory (`cd cscie31-welcome`) and run your geturl file using NodeJS:   `node geturl`

You should see the webpage code written to the console.

## Congratulations!
This completes the set-up you'll need to continue learning NodeJS in this course. We've done a lot:
+ Installed NodeJS locally and ran our first Node program
+ Installed and configured git
+ Created github account and a project
+ Learned to manage code using git and github
+ Created a server in the Digital Ocean cloud
+ Deployed our code to our server


[DO-settings-menu]: img/DO-settings-menu.png
[DO-droplets-new]: img/DO-droplets-new.png
[DO-droplet-ip-address]: img/DO-droplet-ip-address.png
