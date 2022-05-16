# Installation

macOS Catalina (January 2020)

- Updates

- Change preferences

    - Dock > Position on screen: Left
    - Dock > Minimize windows into application icon 
    - Mouse > Secondary click (Click on right side)
    - Siri > Do not show in menu bar
    - Language & Region > Advanced: change decimal character to "."

    - Finder > Preferences > Advanced > Show all filename extensions
    - Finder > Preferences > Advanced > Do not show warning changing extensions
    - Finder > Preferences > Advanced > Keep folders on top when sorting by name

    - Finder > Preferences > Show Hard disks (add HDD to sidebar and hide Hard disks again)
    - Finder > Preferences > Do not show CDs, DVDs, and iPods
    - Finder > Preferences > New Finder window show: Desktop
    - Finder > Preferences > Sidebar: remove not used

    - Safari > View > Show Favorites Bar
    - Safari > Preferences > New windows open with: Top Sites (populate top sites)
    - Safari > Preferences > Top Sites show: 6 sites
    - Safari > Preferences > File download location: Desktop
    - Safari > Preferences > uncheck "Open safe files after downloading"

    - TextEdit > Format > Make Plain Text

- Remove from Dock unwanted applications

- Remove Floating Thumbnail from Screen Shot:

Cmd + Shift + 5 > Options > Show Floating Thumbnail (uncheck)

- Change shell to bash:

```console
$ chsh -s /bin/bash 
$ export BASH_SILENCE_DEPRECATION_WARNING=1
```

- Setup Mail

## Install Xcode from App Store

Launch Xcode and install components
Launch Terminal and type:

    $ xcode-select --install         # agree to license
    $ gcc --version

## From App Store

Applications in iMac Pro

[ Remove Garage Band and iMovie ]

- Adobe Reader
- Anaconda
- Autofirma
- DjView
- Dropbox
- Google Chrome
- Google Earth Pro
- iTerm2
- Keynote, Numbers, Pages
- Macports
- Mendeley
- Microsoft Excel, PowerPoint, Word
- OneDrive
- Papers
- Paraview
- Spotify
- The Unarchiver
- VirtualBox
- Xcode

Additional Applications in MacBook Air

- Brave Browser
- jAmaSeis
- Julia (alternative installation?)
- Mathpix
- Pocket
- qBitorrent
- QGIS3
- Scratch Desktop
- Simple Comic
- VLC

Devel apps:

- Docker
- VirtualBox
- Vagrant
- GRASS
- QGIS

Other software

- XQuartz
- GCC compilers
- Macports
	+ gv
	+ gmt5
	+ coreutils (check that includes gawk)
	+ a2ps
	+ ImageMagick
	+ GraphicsMagick
	+ feh
	+ wget
	+ inetutils (ftp, telnet)
	+ openssh
	+ ffmepg
    + parallel
	[+ libgfortran3 ]
	[+ openmpi ]

Seismology

- SAC
- SEISAN
- CPS
- rdseed
- mstools
- ObsPy / pyrocko

## Install XQuartz

https://www.xquartz.org

[Restart]

## Install Applications

iterm2			https://www.iterm2.com
> Preferences > Profiles > Colors (fff8f0 background, black foreground)
> Preferences > Profiles > Window: 132 x 60

Dropbox			https://www.dropbox.com/install [ DropboxInstaller.dmg ]

Office 365

[ remove unused apps: OneNote, ... ]


- [QGIS](https://qgis.org/en/site/forusers/download.html)
- [Firefox](https://www.mozilla.org/en-US/firefox/new/)
- [Google Earth Pro](https://www.google.com/earth/versions/#earth-pro)
- [VLC](https://www.videolan.org/vlc/index.html)  [ Microsoft_Office_16.33.20011301_Installer.pkg ]
- [DjView](http://djvu.sourceforge.net/djview4.html) [ DjVuLibre-3.5.27+DjView-4.10.6-qt57c-intel64.dmg ]
- [Spotify](https://www.spotify.com/es/download/mac) [ SpotifyInstaller.zip ]
- [VirtualBox](https://www.virtualbox.org)
- [Vagrant](https://www.vagrantup.com)
- [Docker Desktop](https://hub.docker.com/?overlay=onboarding) [ Docker.dmg ]

- Papers			papers_3423_587.dmg + P3-ADUN-IWEF-EFUS-UPIN
- [Mendeley Desktop](https://www.mendeley.com/download-desktop/) [ install plugin for Word ]

- [MacTeX](https://tug.org/mactex/mactex-download.html )
- [TeXstudio](https://www.texstudio.org)
- [Mathpix Snipping Tool](https://mathpix.com/#downloads)

Brave			https://brave.com
qBittorrent
jAmaSeis
Simple Comic
Scratch Desktop


## GMT

If GMT installation with MacPorts fails, GMT can also be installed as an app with a dmg file

To run GMT from the command line (not using the app):

Add the following environmental variables:

    export GMTHOME=/Applications/GMT-6.0.0.app/Contents/Resources
    export PROJ_LIB=$GMTHOME/share/proj6
    export MAGICK_CONFIGURE_PATH=$GMTHOME/lib/GraphicsMagick-1.3.33/config

Add `${GMTHOME}/bin` to `$PATH`


## C/C++ and Fortran

http://hpc.sourceforge.net

    $ sudo tar xvzf gcc-X.X-bin.tar.gz -C /.

For the compiler to find the system headers on Catalina, you may have to specify an additional include path:
-I/Library/Developer/CommandLineTools/SDKs/MacOSX.sdk/usr/include

## Java

Install Java SE (standard Edition) JDK:

https://www.oracle.com/java/technologies/javase-downloads.html
jdk-14.0.2_osx-x64_bin.dmg

## Git

https://www.git-scm.com
Download pkg from https://git-scm.com and install

```console
$ git config --global user.name "Antonio Villasenor"
$ git config --global user.email "antonio.villasenor@csic.es"
$ git config --global color.ui true

$ ssh-keygen -b 4096 -t rsa
[default location, no passphrase]

$ cat ~/.ssh/id_rsa.pub | pbcopy   [ copy key to clipboard ]
```

git completion/prompt

```console
source ~/.git-completion.bash

# colors!
red="\[\033[0;31m\]"
green="\[\033[0;32m\]"
blue="\[\033[0;34m\]"
purple="\[\033[0;35m\]"
cyan="\[\033[0;36m\]"
reset="\[\033[0m\]"

source ~/.git-prompt.sh
export GIT_PS1_SHOWDIRTYSTATE=1
export PS1="$cyan\u@pcanto$green\$(__git_ps1)$blue \W $ $reset"
```
Login to Bitbucket and add key

```console
$ cd
$ mkdir devel
$ cd devel

$ git clone git@bitbucket.org:avillasenorh/let.git
$ git clone git@bitbucket.org:avillasenorh/psim-tools.git
$ git clone git@bitbucket.org:avillasenorh/noise-processing.git
$ git clone git@bitbucket.org:avillasenorh/gtomo.git
```

Login to GitHub and add key

[create .gitignore]

    $ git config --global core.excludesfile ~/.gitignore
    $ ssh-keygen [ -b 4096 -t rsa ]
    $ eval "$(ssh-agent -s)"
    $ ssh-add  ~/.ssh/id_rsa
    $ cat ~/.ssh/id_rsa.pub | pbcopy

Login to BitBucket (https://bitbucket.org/account/signin/)
Preferences > BitBucket settings > SSH keys > Add Key
Description: Mac
Paste Key: cmd + V

    $ cd
    $ mkdir devel
    $ cd devel
    $ git clone git@bitbucket.org:avillasenorh/noise-processing.git
    $ git clone git@bitbucket.org:avillasenorh/psim-tools.git
    $ git clone git@bitbucket.org:avillasenorh/let.git
    $ git clone git@bitbucket.org:avillasenorh/gtomo.git

## Python

Install Anaconda distribution

- Obspy


```
$ conda create -n obspy python=3.7 anaconda [ apparently "basemap" does not work in 3.8 ]
$ conda activate obspy
$ conda install basemap
$ conda install -c conda-forge obspy

[ $ conda install -c conda-forge cartopy ]
```



- TensorFlow 2

```
$  conda create -n tf anaconda [ defaults to 3.7 ]
$  conda activate tf

$  pip -V     [ warning: TensorFlow 2 packages require pip version > 19.0 ]

$  pip install tensorflow
$  pip install keras
```

If you later want to install ObsPy for DL picker:

```
$  conda list hdf5  [ installed ]
$  conda list h5py  [ installed ]

$  conda list graphviz     [ not installed ]
$  conda install graphviz

$  conda list pydot        [ not installed ]
$  conda install pydot

$  conda install -c conda-forge obspy
```


- Intel distribution for Python (IDP)

Do not do "conda config --add channels intel" because this will cause all your Continuum packages
to be replaced with Intel builds, if available. Rather specify "-c intel --no-update-deps" [last option deprecated?]

```console
$ conda create -n idp intelpython3_full python=3 -c intel

  INSTALLED PACKAGE OF SCIKIT-LEARN CAN BE ACCELERATED USING DAAL4PY. 
  PLEASE SET 'USE_DAAL4PY_SKLEARN' ENVIRONMENT VARIABLE TO 'YES' TO ENABLE THE ACCELERATION. 
  FOR EXAMPLE:

      $ USE_DAAL4PY_SKLEARN=YES
```

## Julia

Version installed: Long-term support (LTS) release: v1.0.5 (Sep 9, 2019)

+ Download dmg file from https://julialang.org/downloads/ and install (drag to /Applications)

+ Make a symbolic link:

```
$ ln -s /Applications/Julia-<version>.app/Contents/Resources/julia/bin/julia /usr/local/bin/julia
```


Or install Julia Pro (comes with Juno IDE)

JuliaPro-1.0.5-2_build-54.pkg

    $ sudo ln -s /Applications/JuliaPro-1.0.5-2.app/Contents/Resources/julia/Contents/Resources/julia/bin/julia \
                 /usr/local/bin/julia



## Python and Obspy

$ conda create -n obspy python=3.7
$ conda activate obspy
(obspy)$ conda install -c conda-forge obspy
(obspy)$ conda list basemap        # not installed if conda-forge not added to default channels
(obspy)$ conda install basemap
(obspy)$ conda update -c conda-forge obspy


$ conda create -n mlcourse python=3.7 anaconda
$ conda activate mlcourse

## P
_

1. Create .Prc in home directory:

P=/usr/local/P
TOMO=/data/models/GTOMO
cd $P/data/P.coldef33d
axnu 0 1
set shell
set dpi 300
ns 1 1
nd 1 1

2. Copy P directory to /usr/local


3. Add $P/usrc and $P/Pexec to path in .bashrc 

export P=/usr/local/P
PROGSPATH=${P}/usrc:${P}/Pexec

## CPS

$ tar xvzf NP330.Jun-22-2018.tgz
$ ./Setup OSX40
$ ./C > compile.log 2>&1 &
$ tail -f compile.log

## SEISAN

    $ cd /
    $ sudo mkdir seismo
    $ sudo chown antonio:staff seismo
    $ cd seismo
    $ tar xvzf ..../seisan_macosx_v11.0.tar.gz
    $ cd COM

[edit SEISAN.bash]
export SEISARCH="macosx"
export SEISAN_TOP="/seismo"
fix bad syntax in python aliases

[edit .bashrc]
export SEISAN=/seismo
add source $SEISAN/COM/SEISAN.bash
add ${SEISAN_TOP}/PRO to $PATH

Compiled version requires libgfortran.3.dylib (current version is libgfortran.3.dylib)

$ cd /usr/local/lib
$ sudo ln -s /Users/antonio/anaconda3/pkgs/libgfortran-3.0.1-h93005f0_2/lib/libgfortran.3.dylib

## mstools

src/mstools
$ mkdir -p ~/bin
$ mkdir -p ~/man/man1
$ ./compile_all.sh > compile.log 2>&1

- check that the programs work
- how to access the man pages
