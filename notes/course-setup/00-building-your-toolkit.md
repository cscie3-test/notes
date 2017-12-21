//Readme.md

## Building Your Toolkit
In this course, you'll be writing and testing your code in your "local" environment - meaning on your own computer.  In effect, your computer will be acting as a server - one that you can access from your own browser, but that isn't suitable for access by anyone else.

In the next module, you'll also deploy your code to an internet-based server from which anyone with the URL can access your program.  But for now, let's get the local side of your environment set up.

In the following pages, we're going to do the following steps:

1. Install Node.JS
2. Get familiar with the command-line environment
3. Set up git and github
4. Update NPM
5. Build a Simple Project

### Installation of Node.JS
Node itself is a program that runs on a computer - a program that includes a
Javascript interpreter and some other tools. You can get the appropriate
installer for Node.JS for your computer (Mac or Windows) at
[https://nodejs.org/en/download/](https://nodejs.org/en/download/)

#### Choosing the Correct Version
**LTS**: Node.JS is constantly being updated with major and minor new releases.
In order to provide a stable environment for developers (like you!), some
releases are designated as Long Term Supoort (LTS).  LTS versions continue to
be supported for a while even as new versions of the NodeJS platform continue
to roll out on a regular basis.

Generally the even-numbered releases are the ones destined for LTS.  You can read more about
the LTS strategy on this Node [Foundation article on LTS](https://hackernoon.com/node-js-v6-transitions-to-lts-be7f18c17159),
 and [see the current NodeJS Release Plan](https://github.com/nodejs/Release), which details each release and its
 maintenance schedule.

**Select your platform:**
For simplicity, we recommend the MSI installer for Windows or the .pkg installer for the Mac.

**32- or 64-bit (Windows users):**
If you're on Windows 10, you have a 64-bit operating system.  If you're on an
older version of Windows, [follow the steps in this Microsoft tech note to
determine if you have a 32-bit or 64-bit version] (https://support.microsoft.com/en-us/help/827218/how-to-determine-whether-a-computer-is-running-a-32-bit-version-or-64 )

Follow the instructions to install the software on your computer.

### Getting Used to the Command-line
We're going to be spending a lot of time with the command-line over the next 14 weeks.  The command line is how we'll interact with node itself, the Node Package Manager (npm - more on this later), our version control software (git), and it's how we'll see output and error messages from our code while it's running.  

First, we'll need to do a little tune-up on our command-line environments on both Mac and Windows. This will enable command-line tools like 'git', and if you're on Windows, make the environment a little more Unix-like.

**Mac:** You'll need to install the XCode Command-line Developer Tools.  Simplest way to do this is to enter a Terminal session (find the Terminal application and launch it) and type 'git' at the prompt.  If you already have the Dev Tools installed, you'll see a usage guide for git:

```bash
usage: git [--version] [--help] [-C <path>] [-c name=value]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]        
````
(For reference, you can [view a sample of the full git usage guide](git-usage-guide.md) output from above, but you should also complete the install (if necessary) and try it live on your own computer.)

If you don't have the XCode tools installed, you'll see a prompt that resembles this one (it may say 'git'
rather than 'xcode-select' in the first line):

![mac prompt that you don't have git installed][no-git-prompt]

Select Install and follow the rest of the installation prompts until installation is finished. To confirm that the software is installed, type `git` . You should see the usage guide as shown above.  

**Windows:**
On Windows, we're going to use a customized version of CMDER (pronounced "commander") that's been developed by Harvard's Prof. Susan Buck for the CSCI E15 Dynamic Web Applications course.  You can download this at:  [the Windows-Cmder page in the Dynamic Web Applications course](https://github.com/susanBuck/dwa15-spring2017-notes/blob/master/00_Command_Line/03_Windows-Cmder.md) Follow the directions there for installation.

**Optional Reading:**
 + [CMDER documentation http://cmder.net](http://cmder.net)
 + [CSCI E15 custom version:  https://github.com/susanBuck/cmder](https://github.com/susanBuck/cmder)

#### Video 2.x
Refer to video 2.x in the Canvas course for a brief walk through a few basics of the command line environment. If you're familiar with the command line environment, you can safely skip this step.
We'll look at directory paths, navigating from the command-line, running commands such as
'cd, ls, mkdir,  mv, cp, rm, node, nano`, and also cover wildcards, the escape key and more.

### Try out Node.JS
> Refer to the Canvas course *Try Out Node.JS* page for a walkthrough of running
> your first Node program.

Now with Node installed, let's try it out.  You may recall that the Javascript Console in your browser allows you to directly type and execute Javascript code.  Node provides a similar capability in its REPL (Read-Eval-Print-Loop).  

On your computer, open a command line.  On a Mac, use the Terminal app. If you're using [Windows, look at How to Open Command Prompt](https://www.lifewire.com/how-to-open-command-prompt-2618089) to see how to access the prompt on various versions.

Type `node` at the command prompt.  You should see  something like this:
```Javascript
$ node
>
```

This is essentially the same as the browser's Javascript console with a few differences. Typing `.help` will show you the limited command set for controlling the REPL environment. See the course *Try Out Node.JS* page for more information and a video demo of this functionality.






[no-git-prompt]: ./img/install-xcode-cli-dev-tools500w.png
