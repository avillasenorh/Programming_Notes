# Git

Includes `git`, `GitHub`, `GitLab`, and `BitBucket`.

Initialization
==============

> git config --global user.name "Antonio Villasenor"
> git config --global user.email "antonio@ictja.csic.es"
> git config --global color.ui true

Global .gitignore (in addition to .gitignore in each repository)
================================================================

% vi ~/.gitignore

% git config --global core.excludesfile ~/.gitignore


Configure BitBucket
===================

Generate SSH key
$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/antonio/.ssh/id_rsa):
Created directory '/Users/antonio/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/antonio/.ssh/id_rsa.
Your public key has been saved in /Users/antonio/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:bBA2MN254rYO1BEorwBHzpvW8OxjxnIKFH7AKX4vL8k antonio@dhcp195.ictja.csic.es
The key's randomart image is:
+---[RSA 2048]----+
| .. o+=. .       |
|oo+ .o.+o        |
|o*+o  o  .       |
|= oB...+.        |
| =++=...S        |
|..++. o.         |
|. o.Xo .         |
| . Eoo.          |
|  . .o.          |
+----[SHA256]-----+
$ ls ~/.ssh
id_rsa      id_rsa.pub


Preferences > BitBucket settings > SSH keys > Add Key


Create a repository with existing source code in a new repository directory
============================================================================

- Go to GitHub web page and create the repository with a README.md and a .gitignore

- Go to ~/devel and clone the repository

% cd ~/devel
% git clone https://github.com/avillasenorh/repository

This will create a directory called “repository” with README.md, .gitignore, and .git directory

- Copy source code to repository directory

% cd repository
% cp -r source_directory/* .

% git add -A
% git status
% git commit -m “Initial commit of source code”         # local commit
% git push                                              # send to remote repository (GitHub or Bitbucket)


Create a repository with existing source code in existing source directory
==========================================================================


create a directory called first_repo and make it a repository

to send it to GitHub:

$ git remote add origin https://github.com/gforsyth/first_repo.git
$ git push -u origin master


Installation/configuration 2015-02-20
=====================================

Install Git
git-2.2.1-intel-universal-mavericks.dmg
change path to include /usr/local/git/bin
change path for applications not from command line:
% setup git PATH for non-terminal programs.sh
(creates ~/.MacOSX/environment.plist)

> git config --global user.name "Antonio Villasenor"
> git config --global user.email "antonio@ictja.csic.es"
> git config --global color.ui true


Install GitHub
GitHub for Mac 199.zip (unzip and move GitHub.app to Applications folder)
Open GitHub and login
Install GitHub command line tools

> git config --global credential.helper osxkeychain

This causes GitHub to send an email with SSH key:

The following SSH key was added to your account:

GitHub for Mac - Antonio’s iMac
b1:9e:c4:80:5b:d0:b7:1d:b4:ba:ac:6b:3a:7f:7d:b3

If you believe this key was added in error, you can remove the key and disable
access at the following location:

https://github.com/settings/ssh



Now for example from GitHub application I can clone a repository existing in GitHub to my local disk 
(in directory ~/devel)

How to work with Git/GitHub:

> git add .
> git commit -m "First commit of let-utils repository"
[master (root-commit) 038747f] First commit of let-utils repository
 1 file changed, 177 insertions(+)
 create mode 100644 init1d.c


git clone https://github.com/avillasenorh/github-test.git
cd github-test/
cp ~/src/util_LET/init1d.c .

vi README.md
git commit
git add -A
git commit -m "First commit from local directory"
git push


Installation/configuration 2014-12-23
=====================================

MacBook Pro 15" Retina
OS X 10.9.5 (Mavericks)

Old version of Git already available:

> which git
/usr/bin/git
> git --version
git version 1.9.3 (Apple Git-50)


Download installer from http://git-scm.com/download/mac
git-2.2.1-intel-universal-mavericks.dmg

Add /usr/local/git/bin to $PATH in .cshrc

> which git
/usr/local/git/bin/git
> git --version
git version 2.2.1



> git config --global user.name "Antonio Villasenor"
> git config --global user.email "antonio@ictja.csic.es"
> git config --global color.ui true

Setup a GitHub account with same email address

Account:

avillasenorh + str1...

2 email addresses: avillasenorh@yahoo.es (used to create account)
                   antonio@ictja.csic.es (changed to be the primary one)


ssh-keygen -t rsa -C 'antonio@ictja.csic.es'
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/antonio/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/antonio/.ssh/id_rsa.
Your public key has been saved in /Users/antonio/.ssh/id_rsa.pub.
The key fingerprint is:
3a:09:93:48:38:96:38:41:56:1d:62:7b:a3:c9:90:4a antonio@ictja.csic.es
The key's randomart image is:
+--[ RSA 2048]----+
|oo.+...          |
|oo+ o.           |
|=E.. o           |
|++o.+..          |
|. .++   S        |
|     o o         |
|      +          |
|       .         |
|                 |
+-----------------+


(passphrase was str1...)

> bash
$ eval "$(ssh-agent -s)"
Agent pid 35117

$ssh-add ~/.ssh/id_rsa
Enter passphrase for /Users/antonio/.ssh/id_rsa:
Identity added: /Users/antonio/.ssh/id_rsa (/Users/antonio/.ssh/id_rsa)

$ cat ~/.ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC/GGxSgtpR0fBbdvS1HmcORLRxP7For1aDK9hC5CyDNu4nks348ndbMr/Hs4Ita3iK4xt+T+6u7qQg+1BJhDSk3x1kk+54Cx3S9RHuf3bsi339YllZ487SMTI3bQUgRmObkEgtFiQZwmZR47259WkEI0uUNWNHkI98PKKJzcu7fWP32m2qoaTGVuJdh0pjTiLxu9q/LB+SxpPbKfTImjt8ejcmIosaINlaET4JwukKY3HPK0ddBCRU46/tsUdXehV3ZRxSZICWJDrpjHlLh0L92WAF0OBdnoeYhvB9CH9PUHyPCxhRUInZoBSO50l6kWHZhCKrEiWXY2kyhxs9eU3b antonio@ictja.csic.es

$ cat ~/.ssh/id_rsa.pub | pbcopy


Now go to GitHub web page and login to your account (avillasenorh)
Go to Personal Settings page > SSH keys
Add SSH key
Enter a title: "Antonio's MacBook Pro"
Paste clipboard (ssh key copied to clipboard using pbcopy) in "Key"
Click on "Add key"

To test that process worked, go back to terminal and type:


$ ssh -T git@github.com
Warning: Permanently added the RSA host key for IP address '192.30.252.129' to the list of known hosts.
Hi avillasenorh! You've successfully authenticated, but GitHub does not provide shell access.




===========================================================================================

Connecting over HTTPS:

Cache GitHub password in Git



===========================================================================================
GitHub token

38035823017d17a645c40719317de1f8456d31ed









> git add .
> git commit -m "First commit of let-utils repository"
[master (root-commit) 038747f] First commit of let-utils repository
 1 file changed, 177 insertions(+)
 create mode 100644 init1d.c





   75  16:14   git clone https://github.com/avillasenorh/github-test.git
    76  16:14   ls
    77  16:14   cd github-test/
    78  16:14   ls
    79  16:14   git commit
    80  16:14   h
    81  16:14   cp ~/src/util_LET/init1d.c .
    82  16:14   ls
    83  16:14   vi README.md
    84  16:15   git commit
    85  16:15   git add -A
    86  16:15   git commit
    87  16:15   git commit
    88  16:16   git commit -m "First commit from local directory"
    89  16:18   git push



MacBook Air
===========


which git
/usr/bin/git
32 pcanto:/Users/antonio > git --version
git version 1.9.3 (Apple Git-50)
33 pcanto:/Users/antonio > vi .cshrc
34 pcanto:/Users/antonio > source !$
source .cshrc
35 pcanto:/Users/antonio > git --version
git version 2.2.1
36 pcanto:/Users/antonio > git config --global user.name "Antonio Villasenor"
37 pcanto:/Users/antonio > git config --global user.email "antonio@ictja.csic.es"
38 pcanto:/Users/antonio > git config --global color.ui true
39 pcanto:/Users/antonio > ssh-keygen -t rsa -C 'antonio@ictja.csic.es'
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/antonio/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/antonio/.ssh/id_rsa.
Your public key has been saved in /Users/antonio/.ssh/id_rsa.pub.
The key fingerprint is:
b2:28:07:13:37:ef:89:85:3d:e0:2e:a9:f8:0f:f5:16 antonio@ictja.csic.es
The key's randomart image is:
+--[ RSA 2048]----+
|                 |
|                 |
|  . +            |
|   + *           |
|  o + E S        |
|   * * *         |
|  = = *          |
|.. = .           |
|o....            |
+-----------------+


bash
bash-3.2$ eval "$(ssh-agent -s)"
Agent pid 79771
bash-3.2$ ssh-add ~/.ssh/id_rsa
Enter passphrase for /Users/antonio/.ssh/id_rsa:
Identity added: /Users/antonio/.ssh/id_rsa (/Users/antonio/.ssh/id_rsa)
bash-3.2$ cat ~/.ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDxHl7QJo7Hj6dtjOZW9rjVKx0NG15Bt2bt4Wc1s6T9OqbxRX6wWTeZ6Y5zmAVFteqQksggXiB405LVajmLvyYRicM8x9BtrL0NgirRtSSS+DqoAteg6cBmPXBDKEV7D1Huj01Abbnpoc3MKSkjtUpgo5lvcGbRfVsjkLomth8xbGY62LPrVeHuhPB6dwhnu/lNECYUQsa2ivTmPQoWlkpB1UcktpZvWzBoU4jXSl1DGiP5qkCvBMIbOWn8/x8YTjk/3RKBdyrB3FKQpd1loixuiserwppovnAOXdq5/sBpaJnRAsi9bqPsm17jJr4JBPcj2mfvnnlPF/L4uaNAL8ex antonio@ictja.csic.es
bash-3.2$ cat ~/.ssh/id_rsa.pub | pbcopy
bash-3.2$ ssh -T git@github.com
The authenticity of host 'github.com (192.30.252.130)' can't be established.
RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'github.com,192.30.252.130' (RSA) to the list of known hosts.
Hi avillasenorh! You've successfully authenticated, but GitHub does not provide shell access.


=========================================================================


OLD INSTALLATION



Git/GitHub
==========


https://help.github.com/articles/set-up-git

Download and Install Git
git-1.8.1.3-intel-universal-snow-leopard


Username and email:

% git config --global user.name avillasenorh
% git config --global user.email avillasenorh@yahoo.es

Password caching:

% git credential-osxkeychain
git: 'credential-osxkeychain' is not a git command. See 'git --help'.
% curl -s -O http://github-media-downloads.s3.amazonaws.com/osx/git-credential-osxkeychain
% chmod u+x git-credential-osxkeychain
% sudo mv git-credential-osxkeychain /usr/bin
% git config --global credential.helper osxkeychain
% git credential-osxkeychain
Usage: git credential-osxkeychain <get|store|erase>
