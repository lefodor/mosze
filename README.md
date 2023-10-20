# Using Perforce for version control in game development

## Introduction
The paper focuses on the most important aspects of version control in game development by highlighting the main differences between practices applied in this area and version control practices used at more traditional branches of software development. Furthermore, the paper intends to demonstrate the typical workflow by showing the functionalities of the widely used [Helix Core&trade;](https://www.perforce.com/products/helix-core) from company [Perforce Software](https://www.perforce.com/).  
The paper is structured into three main sections: the first section gives an overview of version control principals and
concepts. The second discusses the main differences between software development and game development and how these translate into practice when it comes to version control.
The following final section showcases the Helix Core&trade; version control software.

## Overview of version control concepts
A proper version control not only requires a system dedicated to this purpose but also the proper use of the system is 
necessary. This is affected by the nature of the development project, team composition and internal practices within the 
development team.

## Version control in game development
Game development is a special branch of software development. Teams working on such projects include not only traditional software developers but also relies heavily on multiple teams of graphical artists, animators responsible for the visual effects of the final product so as designers organising game levels and taking care of the possible interactions
between the game and the players. Furthermore, there might be creative people who are writing the story. All in all, the
complete game development process can be described with terms from software development and other branches like, for example, filmmaking.  

Other important aspect of version control in game development is the way teams go about all the different gaming platforms
currently available on the market. There are games for mobile phones, game consoles and PCs. If the company desires to release the game on several platforms, at some point in time it is necessary to create different main branches for all 
target platforms and maintain and synchronize all of them simultaneously. This may cause issues if some assets are only
applicable to one or another platform versions of the game but not all of them, in this case the given asset or asset changes should only be committed to the main branches of the affected versions. In order to handle such situations, it is imperative to have a robust communication and task management/issue tracking systems within the company such as WIKI or JIRA&trade;. However, all these tools are just facilitating the development process and cannot assure that complications do not come up, so it is also very important to have proper procedures/practices in place within the company and that development teams are constantly reminding themselves to internal development guidelines.

Different branches for different workflows to avoid inflation of repositories (e.g. coders do not need all assets to make their own changes):
* audio
* graphics
* code

### Version control tools used in game development
* GiT Large File System
* Perforce Helix Core
* Unity Plastic SCM

## Setup Helix Core
### Host machine information
```
$ cat /etc/os-release
PRETTY_NAME="Ubuntu 22.04.3 LTS"
NAME="Ubuntu"
VERSION_ID="22.04"
VERSION="22.04.3 LTS (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=jammy
```
## Installation of Helix Core Server and Visual
[Helix](https://help.perforce.com/helix-core/quickstart/Content/quickstart/admin-install-linux.html)  
\cite{Helix}
```

$ wget https://package.perforce.com/perforce.pubkey
$ gpg -n --import --import-options import-show perforce.pubkey
$ gpg -n --import --import-options import-show perforce.pubkey | grep -q "E58131C0AEA7B082C6DC4C937123CB760FF18869" && echo "true"
$ wget -qO - https://package.perforce.com/perforce.pubkey | sudo apt-key add -
$ sudo nano /etc/apt/sources.list.d/perforce.list

# add to the file
deb http://package.perforce.com/apt/ubuntu focal release

$ sudo apt-get update
$ sudo apt-get install helix-p4d
$ sudo /opt/perforce/sbin/configure-helix-p4d.sh

# download p4v (visual interface)
# https://www.perforce.com/downloads/helix-visual-client-p4v

$ export P4PORT=ssl:1666
$ export P4USER=super
$ echo 'export PATH=${PATH}:~/perforce/p4v-2023.3.2495381/bin' >> ~/.bashrc
$ p4 login
$ p4v
```

## Using Helix Core with Godot game engine
[Godot Docs](https://docs.godotengine.org/en/stable/)