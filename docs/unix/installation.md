# Installation

## generic

Install compilers and development tools:

    $ sudo apt-get update
    $ sudo apt-get upgrade
    $ sudo apt-get install build-essential
    $ sudo apt-get install gfortran (?)
    $ sudo apt-get install autotools-dev
    $ sudo apt-get install autoconf

Better use `apt`?

## overflow

Intel compilers (and MPI?)

MPI

    $ sudo apt-get install openmpi-bin openmpi-common openmpi-doc libopenmpi-dev

Google Earth Pro

To install `deb` package beter use `gdebi` instead of `$ sudo dpkg -i example.deb`

    $ sudo apt install gdebi-core # [ wget ] [If you don't have gdebi nor wget]
    $ wget https://dl.google.com/dl/earth/client/current/google-earth-pro-stable_current_amd64.deb
    $ sudo gdebi google-earth-pro-stable_current_amd64.deb 
    $ google-earth-pro

Paraview

### CUDA 11


[Installation Guide](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html)

[CUDA Quick Start Guide](https://docs.nvidia.com/cuda/cuda-quick-start-guide/index.html)

Linux > x86_64 > Ubuntu > 16.04 > deb (local)

```console
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/cuda-ubuntu1604.pin
sudo mv cuda-ubuntu1604.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget http://developer.download.nvidia.com/compute/cuda/11.0.1/local_installers/cuda-repo-ubuntu1604-11-0-local_11.0.1-450.36.06-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu1604-11-0-local_11.0.1-450.36.06-1_amd64.deb
sudo apt-key add /var/cuda-repo-ubuntu1604-11-0-local/7fa2af80.pub
sudo apt-get update
sudo apt-get -y install cuda
```

Linux > x86_64 > Ubuntu > 18.04 > deb (local)

```console
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-ubuntu1804.pin
sudo mv cuda-ubuntu1804.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget http://developer.download.nvidia.com/compute/cuda/11.0.1/local_installers/cuda-repo-ubuntu1804-11-0-local_11.0.1-450.36.06-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu1804-11-0-local_11.0.1-450.36.06-1_amd64.deb
sudo apt-key add /var/cuda-repo-ubuntu1804-11-0-local/7fa2af80.pub
sudo apt-get update
sudo apt-get -y install cuda
```

Linux > x86_64 > Ubuntu > 16.04 > runfile

```console
wget http://developer.download.nvidia.com/compute/cuda/11.0.1/local_installers/cuda_11.0.1_450.36.06_linux.run
sudo sh cuda_11.0.1_450.36.06_linux.run
```

Linux > x86_64 > Ubuntu > 18.04 > runfile

```console
wget http://developer.download.nvidia.com/compute/cuda/11.0.1/local_installers/cuda_11.0.1_450.36.06_linux.run
sudo sh cuda_11.0.1_450.36.06_linux.run
```

## xlr8

    $ sudo synaptic

gv
gfortran
gmt (including all coastlines)

```console
$ sudo addgroup --gid 1001 seismo
Adding group `seismo' (GID 1001) ...
Done.
```

```console
$ sudo adduser --uid 1001 --ingroup seismo antonio
Adding user `antonio' ...
Adding new user `antonio' (1001) with group `seismo' ...
Creating home directory `/home/antonio' ...
Copying files from `/etc/skel' ...
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
Changing the user information for antonio
Enter the new value, or press ENTER for the default
	Full Name []: Antonio Villasenor
	Room Number []: 313
	Work Phone []: 934095410
	Home Phone []:
	Other []:
```

### Install NVIDIA GPU drivers

[Installation of GPU driver was done by Anima]
Instructions [here](http://www.nvidia.com/download/driverResults.aspx/118962/en-us)

Most current driver at 2017-09-15: nvidia-diag-driver-local-repo-ubuntu1604-384.66_1.0-1_amd64.deb

    $ sudo dpkg -i nvidia-diag-driver-local-repo-ubuntu1604-384.66_1.0-1_amd64.deb
    $ sudo apt-get update
    $ apt-get install cuda-drivers

[reboot]

Find out driver version:

```console
$ nvidia-smi
Wed Oct 10 15:08:28 2018
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 410.48                 Driver Version: 410.48                    |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  Tesla P100-PCIE...  Off  | 00000000:81:00.0 Off |                    0 |
| N/A   32C    P0    28W / 250W |      0MiB / 12198MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|  No running processes found                                                 |
+-----------------------------------------------------------------------------+
```


### Install CUDA drivers and CUDA Toolkit

[Checks in http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html]

    $ sudo dpkg -i cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64.deb
    $ sudo apt-get update
    $ sudo apt-get install cuda

Install CUDA 9.0

    $ sudo dpkg -i cuda-repo-ubuntu1604-9-0-local_9.0.176-1_amd64.deb
    $ sudo apt-key add /var/cuda-repo-9-0-local/7fa2af80.pub
    $ sudo apt-get update           # if you do this it installs latest cuda
    $ sudo apt-get install cuda

[gives may warnings, including system not bootable!!??]


Try again usin runfile:

    $ sudo sh cuda_9.0.176_384.81_linux.run

Check CUDA version:

```console
$ nvcc -V
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2018 NVIDIA Corporation
Built on Sat_Aug_25_21:08:01_CDT_2018
Cuda compilation tools, release 10.0, V10.0.130
```

Changing symbolic link to /usr/local/cuda:

```console
antonio@xlr8 ~ $ nvcc -V
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2017 NVIDIA Corporation
Built on Fri_Sep__1_21:08:03_CDT_2017
Cuda compilation tools, release 9.0, V9.0.176
```


### Install Intel compilers


$ ./install_GUI.sh (not as sudo, it will ask later for password)
[install it as trial!]
[options: disable IA32 - if not 32-bit libraries error, and compiler does not install]

### MPI

OpenMPI:
synaptic -> openmpi-bin libopenmpi-dev (selecting the second one also selects the first one)

Intel:
$ tar xvzf l_mpi_2017.2.174.tgz
$ cd l_mpi_2017.2.174.tgz
$ sudo ./install.sh
[enter defaults]
Install location: /opt/intel/parallel_studio_xe_2017.2.050

### Install PGI compiler

$ tar xvzf pgilinux-2017-175-x86_64.tar.gz
$ sudo ./install

[installs PGI CUDA but not MPI]

$ cd /opt/pgi
[rename or delete license.dat]
[copy license.dat provided by CSIC]


Edit .bashrc

export PGI=/opt/pgi;
export PATH=/opt/pgi/linux86-64/17.5/bin:$PATH;
export MANPATH=$MANPATH:/opt/pgi/linux86-64/17.5/man;
export LM_LICENSE_FILE=$LM_LICENSE_FILE:/opt/pgi/license.dat;


Command pgi_license_tool can manage licenses

$ sudo ln -s /lib64/ld-linux-x86-64.so.2 /lib64/ld-lsb-x86-64.so.3
$ pgi_license_tool [option 4 = do nothing ]


### Install Python

Install python 3.5 with last installer that came with 3.5 by default (Anaconda3-4.2.0)

$ bash Anaconda3-4.2.0-Linux-x86_64.sh

$ conda update conda
$ conda update anaconda
$ conda install accelerate


### Setup GitHub for git

```console
$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/antonio/.ssh/id_rsa):
Created directory '/home/antonio/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/antonio/.ssh/id_rsa.
Your public key has been saved in /home/antonio/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:abLlSOEd7acuBNIeH0JokgLIZwkcyMQYNKNke4ll2Ns antonio@xlr8
The key's randomart image is:
+---[RSA 2048]----+
|#@=+..           |
|O*X=+ .  .       |
|.+o=oo. . .      |
|  ...E=o.+       |
|     o+=S.. .    |
|     ..Bo  o     |
|      o.. .      |
|        ..       |
|         ..      |
+----[SHA256]-----+
```

NO PASSPHRASE!!!!

    $ cat ~/.ssh/id_rsa.pub


[go to Bitbucket web page, Settings > "SSH keys > Add Key" and add public key]


To check that it worked:

```console
$ ssh -T git@bitbucket.org
The authenticity of host 'bitbucket.org (104.192.143.2)' can't be established.
RSA key fingerprint is SHA256:zzXQOXSRBEiUtuE8AikJYKwbHaxvSc0ojez9YXaGp1A.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'bitbucket.org,104.192.143.2' (RSA) to the list of known hosts.
logged in as avillasenorh.
```

You can use git or hg to connect to Bitbucket. Shell access is disabled.


    $ cd
    $ mkdir bin scripts devel
    $ cd devel
    $ git clone git@bitbucket.org:avillasenorh/noise-processing.git
    $ git clone git@bitbucket.org:avillasenorh/psim-tools.git
    $ git clone git@bitbucket.org:avillasenorh/let.git


### Install locally FFTW

    $ cd
    $ mkdir -p lib/fftw

[download fftw-3.3.6-pl2.tar.gz]

```console
$ cd
$ cd src
$ tar xvzf .../fftw-3.3.6-pl2.tar.gz
$ cd fftw-3.3.6-pl2
$ ./configure --prefix=/home/antonio/lib/fftw
$ make
$ make check
(basic tests passed)
$ make install
.
.
.
----------------------------------------------------------------------
Libraries have been installed in:
   /home/antonio/lib/fftw/lib

If you ever happen to want to link against installed libraries
in a given directory, LIBDIR, you must either use libtool, and
specify the full pathname of the library, or use the '-LLIBDIR'
flag during linking and do at least one of the following:
   - add LIBDIR to the 'LD_LIBRARY_PATH' environment variable
     during execution
   - add LIBDIR to the 'LD_RUN_PATH' environment variable
     during linking
   - use the '-Wl,-rpath -Wl,LIBDIR' linker flag
   - have your system administrator add LIBDIR to '/etc/ld.so.conf'

See any operating system documentation about shared libraries for
more information, such as the ld(1) and ld.so(8) manual pages.
----------------------------------------------------------------------
.
.
.
```


### Install packages with Synaptic

- gcc/gfortran
- gv
- GMT5
- libncurses-dev for CPS
- zlib for mseed2sac

