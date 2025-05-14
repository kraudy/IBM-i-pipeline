# IBM-i-pipeline
This is intended to give a guideline on using a modern [IBM I](https://en.wikipedia.org/wiki/IBM_i) Pipeline.
Some knowledge about [ILE](http://en.wikipedia.org/wiki/Integrated_Language_Environment), [PASE](https://en.wikipedia.org/wiki/IBM_i#PASE), Git and Linux is helpfull but not necessary. I'll make another repo for those.

Modern developments are usually done on Linux or Mac but most IBM I developer usually have a Windows OS and from that they connect to the Power([AS/400](https://en.wikipedia.org/wiki/IBM_AS/400), iSeries) using [ACS](https://www.ibm.com/support/pages/ibm-i-access-client-solutions) (Access Client Solutions) with a [5250 Termianl emulator](https://en.wikipedia.org/wiki/IBM_5250) over telnet.  

Once inside, the IBM I developer needs to do what he was created to do: Write some code; for that we have [SEU](https://www.nicklitten.com/course/what-is-seu-source-entry-utility/) (Source entry utility or stone age entry utility ), [RDI](https://www.nicklitten.com/module/rational-developer-rdi/) (Rational Developer for I) or (the modern one) [VsCode](https://code.visualstudio.com/). Nick Litten has a nice resume about this on his blog [
Windows Setup for IBM i Developers](https://www.nicklitten.com/windows-setup-ibm-developers/) 

Here, we take the Linux (Ubuntu) approach from Windows, using [WSL](https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux) and VsCode.

What else do we need? Well, a Power Server, which  is actually a very important requirement. Since we don't have one or can't buy one, we will be using [PUB400](https://pub400.com/), which, luckily, is a free Power Server on the internet. 

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

For this part you need to have set up the github ssh keys. Clone the repo to the cool dir and cd into it.

```bash
git clone git@github.com:Your_User/Your_cool_repo.git
cd ./Your_cool_repo
```

That's it, you can do a ```git status``` to check.

## Create dir struct

We need a directory struct that let us have multiple ibm i projects inside the same git repo
```bash
mkdir empty
mkdir simple
mkdir lil_complex
```

## Create empty project



### Commit changes

## Create simple project

### Commit changes

### Compile

### Run

## Create lil_complex project

### Commit changes

### Compile

### Run