# IBM-i-pipeline
This is intended to give a guideline on using a modern IBM I Pipeline to someone who already have some knowledge about ILE and PASE environments. Git and Linux knowdledge is also helpfull.

Modern developments are usually done on Linux or Mac but most IBM I developer usually have a Windows OS and from that they connect to the Power using [ACS](https://www.ibm.com/support/pages/ibm-i-access-client-solutions) (Access Client Solutions), [SEU](https://www.nicklitten.com/course/what-is-seu-source-entry-utility/) (Source entry utility or stone age entry utility ), [RDI](https://www.nicklitten.com/module/rational-developer-rdi/) (Rational Developer for I) or (the modern ones) [VsCode](https://code.visualstudio.com/). Nick Litten has a nice resume about this on his blog [
Windows Setup for IBM i Developers](https://www.nicklitten.com/windows-setup-ibm-developers/) 
Here, we take the Linux approach from Windows, using [WSL](https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux).

What we need: 
- [WSL Ubuntu](https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux)
- [ACS](https://www.ibm.com/support/pages/ibm-i-access-client-solutions)
- [VsCode](https://code.visualstudio.com/)
- [Code for IBM I](https://codefori.github.io/docs/)
- [IBM I proyect explorer](https://marketplace.visualstudio.com/items?itemName=IBM.vscode-ibmi-projectexplorer)
- [PUB400 User](https://pub400.com/)