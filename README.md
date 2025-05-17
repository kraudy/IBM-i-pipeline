# IBM-i-pipeline
This is intended to give a guideline on using a modern [IBM I](https://en.wikipedia.org/wiki/IBM_i) Pipeline.
Some knowledge about [ILE](http://en.wikipedia.org/wiki/Integrated_Language_Environment), [PASE](https://en.wikipedia.org/wiki/IBM_i#PASE), Git and Linux is helpfull but not necessary.

Modern developments are usually done on Linux or Mac but most IBM I developer usually have a Windows OS and from that they connect to the Power([AS/400](https://en.wikipedia.org/wiki/IBM_AS/400), iSeries) using [ACS](https://www.ibm.com/support/pages/ibm-i-access-client-solutions) (Access Client Solutions) with a [5250 Terminal emulator](https://en.wikipedia.org/wiki/IBM_5250) over telnet.  

Once inside the Power, the IBM I developer needs to do what he was created to do: Write some cool code that will run for the ages. For that we have [SEU](https://www.nicklitten.com/course/what-is-seu-source-entry-utility/) (Source entry utility or stone age entry utility ), [RDI](https://www.nicklitten.com/module/rational-developer-rdi/) (Rational Developer for I) or (the modern one) [VsCode](https://code.visualstudio.com/). 

Nick Litten has a nice resume about these tools on his blog [
Windows Setup for IBM i Developers](https://www.nicklitten.com/windows-setup-ibm-developers/). Here, we take the Linux (Ubuntu) approach from Windows, using [WSL](https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux) and VsCode.

What else do we need? Well, a Power Server, which  is actually a very important requirement. Since we don't have one or can't buy one, we will be using [PUB400](https://pub400.com/), which, luckily for us, is a free Power Server on the internet. Nice! Shout out to our boys at pub400. 

If you need help setting up ACS, [putty](https://en.wikipedia.org/wiki/PuTTY) or Code for IBM i with PUB400, here is a nice [tutorial by Marco](https://github.com/MarcoDeSenas/IBMi-topics-thanks-to-pub400/blob/main/HowTo/Workstation%20tools.md) about it. 

Here is a list: 
- [WSL Ubuntu](https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux)
- [ACS](https://www.ibm.com/support/pages/ibm-i-access-client-solutions)
- [VsCode](https://code.visualstudio.com/)
  - [Code for IBM I](https://codefori.github.io/docs/)
  - [IBM I project explorer](https://marketplace.visualstudio.com/items?itemName=IBM.vscode-ibmi-projectexplorer)
  - [Remote WSL](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl)
- [PUB400 User](https://pub400.com/cgi/signup.nd/start)


## Create repo

Just go to your github account and on the Repositories tab click New, create the new repo with a readme and maybe a MIT liscense if you feel like so.

Now open you WSL from VsCode using the Remote WSL plugin. Create a dir, cd into it.

```bash
mkdir $HOME/cool_ibm
cd $HOME/cool_ibm
```

For this part you need to have set up the github ssh keys. If you need some guidance with this, i'll hook you up. Sanjula has a good [git concepts tutorial](https://github.com/SanjulaGanepola/ibmi-talks/tree/main/Git%20Concepts%20I%20Wish%20I%20Knew%20Years%20Ago) for ibmers and non-ibmers if you need some background.

Clone the repo to the cool dir, cd into it and set up a vscode [workspace](https://code.visualstudio.com/docs/editing/workspaces/workspaces) (optional but is very useful).


```bash
git clone git@github.com:Your_User/Your_cool_repo.git
cd ./Your_cool_repo
```

That's it, you can do a `git status` to check.

## Create repo dir struct

We need a directory struct that let us have multiple ibm i projects inside the same git repo... because that's how i roll.

```bash
mkdir ./empty && mkdir ./simple && mkdir ./lil_complex
```

Add these folders to your workspace on VsCode (File -> Add Folder to Workspace)

## Create empty project

So, this is the simplest ibm i project that you can make, no source code for now.

In the ibm i project explorer select the empty dir and create the configuration files, it automaitcally creates two files: `.gitignore` and `.iproj.json`.

.gitignore
```bash
.logs
.evfevent
.env
```

.iproj.json
```json
{
  "description": "Empty project"
}
```

We actually don't need this `.gitignore` since we already have one in our repo but you can add the ignored extensions to that.

If you want to do it manually just create the `iproj.json` file inside the `./empty` dir and the ibm i project explorer will detect it. That's it.

### Commit changes

Now we need to sync the local changes with our github repo. This is the idea: Check what have changed, add it to the staged area, commit it and push it to your github repo. Very simple

```bash
git status # Take a peek
git add .  # Add all to the staged area
git commit -m "My cool ibm i project" # Commit the staged changes with a descriptive message
git push   # Send it to your github repo
```

## Create simple project

We already created the simplest project, an empty one, now we'll create a simple one.

Use the ibm i project explorer to initialize the `./simple` project like we did with the empty one.

Lets create a dir that represents a source phisical file (IBM I Intro repo here soon) and cd into it.

```bash
cd ./simple
mkdir ./qrpglesrc && cd ./qrpglesrc
```

### Create first source

Add our [RPG](https://en.wikipedia.org/wiki/IBM_RPG) (RPG intro repo here) hello world source. Note the naming convention, our pipeline will use that name to know how to compile the soure `rpgle -> languaje` `pgm -> ibm i object`.

```bash
touch hello.pgm.rpgle
```

Now, the code; don't worry if it looks kind of cryptic for you. I gotcha (RPG intro repo here)

```rpg
**free
Ctl-opt DftActGrp(*No);
Dsply 'Hello world!, edited';
*inlr = *on;
return;
```

That is our first source file. Nice!

### Compile

Now, how to compile it?.

First, connect to PUB400 with the code for ibm i plugin.
On the ibm i project explorer go to the simple project and set the deploy location, sould look something like this

```bash
/home/Your_User/builds/simple
```

Select the deploy method, compare should be fine.

Also, this automatically generates a .env for your project that looks similar to this, which is basically a library list for the job on the ibm i (don't worry about these definitions if you don't know them)

```bash
LIBL=QGPL QTEMP GAMES400
```

Now set the data_library variable, this can be any of the two libraries that PUB400 gives you. It will be added to the .env file.

```bash
data_library=Your_Library
```

Make sure Your_Library is in the library list of the ibm i project and set it to current library.

By this point we are ready to compile the hello world.

Go to the simple ibm i project and hit run, then select Run build.

It will ask you to set the build command, the default is `makei build` that should be fine since we are using [BOB](https://github.com/IBM/ibmi-bob). It will deploy the source and look for a Rules.mk file in the project root, which we don't have, lets make it.

You can make a template with the command `makei init` directly on PASE. It will take you through some steps that creates an `iproj.json` file for the project (we already have it), an empty `Rules.mk` file (with only `SUBDIRS :=`) and other config. The Rules.mk file tells bob the dir struct inside your project. We are going to do it manually, go to your project root and creat it

```bash
cd ..
touch Rules.mk
```

Now add the dirs of your project with the source file like this, we only have one

```bash
SUBDIRS = qrpglesrc
```

Hit run again in the ibm i simple project. But... it still didn't build our program, we need one more thing.

Each source dir need a Rules.mk that tell bob what it needs to build.

```bash
cd qrpglesrc/
touch Rules.mk
```

Add this simple Makefile notation

```bash
HELLO.PGM: hello.pgm.rpgle
```

That's it, it shuld be a success and look something like this. If you look closely we are actually using `make` under the hood.

```bash
Running Action: makei build (Time PM)
Working directory: /home/Your_User/builds/simple
Commands:
	makei build

> /QOpenSys/pkgs/bin/make -k BUILDVARSMKPATH="/tmp/tmpu5na7fv9" -k BOB="/QOpenSys/pkgs/lib/bob" -f "/QOpenSys/pkgs/lib/bob/src/mk/Makefile" all
=== Creating Bound RPG Program [HELLO] in Your_Library
CRTBNDRPG srcstmf('/home/Your_User/builds/simple/qrpglesrc/hello.pgm.rpgle') PGM(Your_Library/HELLO) TGTCCSID(*JOB) DBGVIEW(*ALL) OPTION(*EVENTF) TEXT('') INCDIR(*NONE)
✓ HELLO.PGM was created successfully!

Objects:             0 failed 1 succeed 1 total
Build Completed!
```

You can find the compiler output (Spool file) at `.../simple/.logs`

### Run

Log in to your PUB400 account using ACS 5250 terminal emulator, change the curlib, go to your library and call the Hello program

```bash
chgcurlib Your_Lib
wrklibpdm Your_Lib
OP 12
OP 16
```

You should see something like this

```bash
DSPLY  Hello world                                   
```

Commit your changes and push them to the github repo.

## Create lil_complex project

Now we create a little more complex project structure.

We will be using Edmund [Payroll project](https://github.com/edmundreinhardt/payroll-from-qsys/tree/main). You can just clone it to another dir and then copy the dir struct with `cp`. If you decide to clone it here, directly, you will need to delete the git file to keep our idea of having only one repo with many projects. We are doing it the manual way for learning sake.

Lets use a cool git functionality, a branch (Git, under the hood is actually the [Merkle tree](https://en.wikipedia.org/wiki/Merkle_tree) algorithm, if you are into that kind of thing). Since we are gonna do a little bigger change this time, lets use a branch in case we break something (This is what you usually do on bigger projects or when you want to try something kinda wild).

```bash
cd ../../ # Go to your repo root
git switch -c lil_complex # This creates the new branch and changes you to it. You can also do `git checkout` but i don't like that.
git branch # Check that you are actually on the new lil_complex branch.
```

This is our dir struct

```bash
cd ./lil_complex
mkdir ./qddssrc && mkdir ./qrpglesrc && mkdir ./qsqlsrc
touch ./qddssrc/Rules.mk && touch ./qrpglesrc/Rules.mk && touch ./qsqlsrc/Rules.mk
```

Create the `Rules.mk` file of the project.

```bash
touch ./Rules.mk && echo "SUBDIRS = qddssrc qrpglesrc qsqlsrc" > ./Rules.mk
```

Go to lil_complex project on the ibm project explorer. On Variables set the data libary, on Source set the deploy location, something like this `/home/Your_User/builds/lil_complex` and deploy. (AIX intro here)

Go to the deployed location on the IFS browser of code for ibm i, rigth click `Open terminal here`. This should open a new terminal inside your VsCode. Now, you have the terminal of your WSL alongside the PASE terminal on the remote Power. As you may tell, that is really nice, we should be grateful to our Code for IBM I friends.

Lets do a little check for `makei`

```bash
ls -l /QOpenSys/pkgs/bin/makei # You can check if it exist like hits
# lrwxrwxrwx 1 qsys 0 64 Jan  6 14:43 /QOpenSys/pkgs/bin/makei -> /QOpenSys/pkgs/lib/bob/bin/makei
-bash-5.2$ which makei
#/QOpenSys/pkgs/bin/makei <--- This should be the output
```

If `which makei` does not works, you may need to set up a `.profile` on your home dir at `/home/Your_User/`

```bash
touch ./.profile && echo "export PATH=/QOpenSys/pkgs/bin:$PATH" > ./.profile
```

If you want to try `makei init` here just for the gigs, delete the `iproj.json` and go ahead. After that just redeploy the project if you don't like the changes.

### Making the make

So far, we have the lil_complex project almost complete, now we need to tell bob how to build it each source on each dir. We can have a specific configuration for each source dir with a `.ibmi.json` file but is not necessary here.
Sample `.ibmi.json`
```json
{
  "build": {
    "tgtCcsid": "37",
  }
}
```

`Rules.mk` uses the same notation as Makefiles which is basically `Object to build: dependencies needed`. Here are the bob's [docs](https://ibm.github.io/ibmi-bob/#/prepare-the-project/rules.mk)

```bash
echo "MSTDSP.FILE: mstdsp.dspf EMPMST.FILE PRJMST.FILE RSNMST.FILE" > ./qddssrc/Rules.mk 
echo "PAYROLL.PGM: payroll.pgm.rpgle MSTDSP.FILE EMPMST.FILE PRJMST.FILE RSNMST.FILE" > ./qrpglesrc/Rules.mk 
echo -e "EMPMST.FILE: empmst.table \nPRJMST.FILE: prjmst.table \nRSNMST.FILE: rsnmst.table" > ./qsqlsrc/Rules.mk
```

It should compile with no problem. If you got an issue check that your &curlib on the ibm project explorer is set.

### Commit changes

Remember that we are on another branch. Everything works so now we want the changes on the main brach

```bash
git status # check what has changed
git diff # if you want to see the changes
git add --all # add everthing, don't look back
git commit -m "Complete cool lil project" 
git push
```

`git push` should not work. Change to your main branch, do a merge, push and delete the lil_proyect branch

```bash
git switch master # Note how the dir struct changes. The magic of git
git merge lil_complex # The changes are back!
git push # Changes to github
git branch -d lil_complex # Delete it, we don't need it anymore. The branch life cycle.
```

That's it!

## Wrapping up

If you have any suggestions make an issue and i'll check it out. Thanks.
