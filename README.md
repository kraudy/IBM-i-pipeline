# IBM-i-pipeline
This is intended to give a guideline on using a modern IBM I Pipeline.
Some knowledge about ILE, PASE, Git and Linux is helpfull but not necessary. I'll make another repo for those.

Modern developments are usually done on Linux or Mac but most IBM I developer usually have a Windows OS and from that they connect to the Power using [ACS](https://www.ibm.com/support/pages/ibm-i-access-client-solutions) (Access Client Solutions), [SEU](https://www.nicklitten.com/course/what-is-seu-source-entry-utility/) (Source entry utility or stone age entry utility ), [RDI](https://www.nicklitten.com/module/rational-developer-rdi/) (Rational Developer for I) or (the modern ones) [VsCode](https://code.visualstudio.com/). Nick Litten has a nice resume about this on his blog [
Windows Setup for IBM i Developers](https://www.nicklitten.com/windows-setup-ibm-developers/) 
Here, we take the Linux approach from Windows, using [WSL](https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux).

What we need: 
- [WSL Ubuntu](https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux)
- [ACS](https://www.ibm.com/support/pages/ibm-i-access-client-solutions)
- [VsCode](https://code.visualstudio.com/)
- [Code for IBM I](https://codefori.github.io/docs/)
- [IBM I project explorer](https://marketplace.visualstudio.com/items?itemName=IBM.vscode-ibmi-projectexplorer)
- [PUB400 User](https://pub400.com/)

## Create repo

We simply create a github repo and clone it to our Ubuntu WSL

```bash
git clone git@github.com:Your_User/Your_repo.git
```

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