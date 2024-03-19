# Admin

Umount a non-responsive NFS file system:

    $ sudo umount -f -l /filesystem


Ubuntu commands for creating and deleting users

    $ sudo addgroup --gid 1001 seismo
    $ sudo addgroup --gid 3850 sismi

    $ sudo adduser --uid 3801 --ingroup sismi --shell /bin/tcsh jdiaz
    $ sudo adduser --uid 3807 --ingroup sismi mario (bash shell)

    $ sudo adduser --home /data9/INPUT input (non-standard home directory)

Remove an user and all its files (Ubuntu)

    $ sudo deluser --remove-all-files user & (can take some time, so better send to background)


Get IPs and MAC addresses in a local network

    $ ifconfig | grep broadcast | arp -a  

## SSH keys

Install a public key to login remotely

```console
$ ssh-keygen -b 4096 -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/antonio/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/antonio/.ssh/id_rsa.
Your public key has been saved in /Users/antonio/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:Lfbjv4MWIq0MRc7nkL8KYcIGLiEEYyfuTD3NuzkV9Uk antonio@passavol2.cmima.csic.es
The key's randomart image is:
+---[RSA 4096]----+
|++ .     . E     |
|+.+ o . . o .    |
|+o o * o   o     |
|*+  . B o.       |
|.++ oo BS .      |
|.. o..=.=o.      |
|    .* o ooo     |
|     .+ ..o..    |
|      .. ...oo   |
+----[SHA256]-----+
```

```console
$ ssh-copy-id antonio@edge3.ictja.csic.es
/opt/local/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/Users/antonio/.ssh/id_rsa.pub"
The authenticity of host 'edge3.ictja.csic.es (193.144.102.105)' can't be established.
ECDSA key fingerprint is SHA256:eMm9bMReccDbOesNDlt9Lf6VMYuv1XlccefWC8zynaA.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
/opt/local/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/opt/local/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
antonio@edge3.ictja.csic.es's password:

Number of key(s) added:        1

Now try logging into the machine, with:   "ssh 'antonio@edge3.ictja.csic.es'"
and check to make sure that only the key(s) you wanted were added.
```

## Disable suspend and hibernation

Instructions in this [link](https://www.tecmint.com/disable-suspend-and-hibernation-in-linux/).

```
$ sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target

Created symlink /etc/systemd/system/sleep.target → /dev/null.
Created symlink /etc/systemd/system/suspend.target → /dev/null.
Created symlink /etc/systemd/system/hibernate.target → /dev/null.
Created symlink /etc/systemd/system/hybrid-sleep.target → /dev/null.
```

Verify changes:

    $ sudo systemctl status sleep.target suspend.target hibernate.target hybrid-sleep.target

and reboot (or $ sudo systemctl restart systemd-logind.service)

Re-enable suspend and hibernation:

```
$ sudo systemctl unmask sleep.target suspend.target hibernate.target hybrid-sleep.target

Removed /etc/systemd/system/sleep.target.
Removed /etc/systemd/system/suspend.target.
Removed /etc/systemd/system/hibernate.target.
Removed /etc/systemd/system/hybrid-sleep.target.
```

Verify:

    $ sudo systemctl status sleep.target suspend.target hibernate.target hybrid-sleep.target

## MySQL

Install MySQL from command line (not tested)

    $ sudo apt-get -y install mysql-server mysql-client
    $ sudo mysql_secure_installation

(Probably this does not install "dev" package with include and libraries for MySQL)

Setup password for mysql root

    ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root_password';

## Mount exFAT volumes in Ubuntu Linux

Ubuntu by default is not able to mount disks formatted in exFAT

    $ sudo apt-get install exfat-fuse exfat-utils

## Better Linux tools for sysadmin

```
htop/atop > top
ss > netstat
ip > ifconfig
dig > nslookup
mtr > ping+traceroute
collectl > sar
```

## Update GCC

Default version of gcc/g++ in xlr8 (Ubuntu 14.04 LTS) is 5.4.0

Need at least version 7 to compile Mirmex

To fix some problems with corrupted packages:

    $ sudo rm -vf /var/lib/apt/lists/*
    $ sudo apt-get update

(still gives an error about Google Earth, but the rest seems to work fine)

```console
$ sudo add-apt-repository ppa:ubuntu-toolchain-r/test

$ sudo apt-get update

$ sudo apt install gcc-7 g++-7

$ sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 70 \
 --slave /usr/bin/g++ g++ /usr/bin/g++-7 \
 --slave /usr/bin/gcov gcov /usr/bin/gcov-7
```

(Modified from this [link](https://linuxize.com/post/how-to-install-gcc-compiler-on-ubuntu-18-04/)):

```console
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 90 --slave /usr/bin/g++ g++ /usr/bin/g++-9 --slave /usr/bin/gcov gcov /usr/bin/gcov-9
```

WARNING!!!: gfortran not updated to version 7!!!
