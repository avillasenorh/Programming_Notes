## Fresh macOS Ventura installation

### 1. Go to App Store to get installer

Once the download has completed it will ask you to install the update.
Do not press continue, instead quit the program.

### 2. Format pen drive for installation

Open the application **Disk Utility**

Select `View > Show all devices`. This makes available the `GUID partition` option.
 
Select the first option for disk format. **WARNING**: do not use APFS (some tutorials are wrong).

Call the new partition on the pen drive `Untitled`. Later it will be latter renamed to
"Install macOS Venture".

### 3. Make the pen drive bootable

Enter the following command:

```
$ sudo /Applications/Install\ macOS\ Ventura.app/Contents/Resources/createinstallmedia --volume /Volumes/Untitled
Password:
Ready to start.
To continue we need to erase the volume at /Volumes/Untitled.
If you wish to continue type (Y) then press return: Y
Erasing disk: 0%... 10%... 20%... 30%... 100%
Copying essential files...
Copying the macOS RecoveryOS...
Making disk bootable...
Copying to disk: 0%... 10%... 20%... 30%... 40%... 50%... 60%... 70%... 80%... 90%... 100%
Install media now available at "/Volumes/Install macOS Ventura"
```

### 4. Allow booting from an external disk

Reboot the computer in _recovery mode_ by pressing `cmd + R`.
This might ask you to enter the password a couple of times.

Go to `Utilities > Startup security utility` and select
`Allow booting from external of removable media`.

Insert the pen drive in the computer and reboot again to _Startup Manager_ by pressing
the `opt` key, and select the `Install macOS Monterrey` drive.

For a fresh installation you need to go first to `Disk Utility` and erase the disk.
If not it simply upgrades the operating system.

After erasing the disk select `Install macOS Monterrey` (**WARNING**: and additional update might be
required in order to use the bootable external disk).

Once the installation process has started, accept the terms and select `Install in Macintosh HD`.

### 5. Install development tools

#### `bash`

Because of license issues, in the latest versions of macOS the default shell is `zsh` instead of `bash`.
To change the default shell to `bash` and silence the deprecation warning open a terminal and type:

    $ chsh -s /bin/bash
    $ export BASH_SILENCE_DEPRECATION_WARNING=1

Initially (before creating/modifying the `.bash_profile` and `.bashrc` files)
the `$PATH` environmental variable is set to:

    /usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin


Because of those license issues, the version of `bash` provided in `/bin/bash`
is very old (3.2, from 2007!)

```
$ echo $BASH_VERSION
3.2.57(1)-release

$ /bin/bash --version
GNU bash, version 3.2.57(1)-release (x86_64-apple-darwin21)
Copyright (C) 2007 Free Software Foundation, Inc.
```

Once you install Macports and a few packages, a newer version of `bash` will be available in 
`/opt/local/bin/bash`:

```
$ /opt/local/bin/bash --version
GNU bash, version 5.1.16(1)-release (x86_64-apple-darwin21.1.0)
Copyright (C) 2020 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>

This is free software; you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
```

To make this `bash` the default, add `/opt/local/bin/bash` to the `/etc/shells` file:

```
$ sudo vi /etc/shells

$ cat /etc/shells
# List of acceptable shells for chpass(1).
# Ftpd will not allow users to connect who are not using
# one of these shells.

/bin/bash
/opt/local/bin/bash
/bin/csh
/bin/dash
/bin/ksh
/bin/sh
/bin/tcsh
/bin/zsh
```

and then:

    $ chsh -s /opt/local/bin/bash

To use this shell in shell scripts, replace the common shebang `#!/bin/bash` for:

    #!/usr/bin/env bash


#### XCode

Go to App Store and install **XCode**. Once it is installed, open it and it will install the
**Command line tools**. If the tools are not installed automatically it can be done from the command line:

```
$ xcode-select --install         # agree to license
$ gcc --version
Configured with: --prefix=/Applications/Xcode.app/Contents/Developer/usr --with-gxx-include-dir=/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX.sdk/usr/include/c++/4.2.1
Apple clang version 13.0.0 (clang-1300.0.29.30)
Target: x86_64-apple-darwin21.3.0
Thread model: posix
InstalledDir: /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin
```

After the installation of **XCode**, the `$PATH` variable is expanded to:

    /usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Library/Apple/usr/bin

#### XQuartz

Then install [XQuartz](https://www.xquartz.org) for X Window support. After the
installation of **XQuartz** the `$PATH` variable is expanded to:

    /usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/opt/X11/bin:/Library/Apple/usr/bin

#### GCC C and Fortran compilers

Install `gcc` and `gfortran` compilers from the [HPC Mac OS X](http://hpc.sourceforge.net)
web page. Download the appropriate `.tar.gz` file (as of January 2022, the version for Monterrey
was `gcc-11.2-bin.tar.gz`). To install it, simply type:

```
$ sudo tar xvf gcc-11.2-bin.tar -C /.

$ gcc --version
gcc (GCC) 11.2.0
Copyright (C) 2021 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

$ gfortran --version
GNU Fortran (GCC) 11.2.0
Copyright (C) 2021 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

#### Setup dotfiles

At this point it is convenient to setup the `.bash_profile` and `.bashrc` files.
Initially `.bash_profile` contains simply:

```
#
if [ -f ~/.bashrc ]; then
	. ~/.bashrc
fi
```

**Important**: unlike in Linux, in macOS all the new terminals are login terminals, so they 
all run `.bash_profile`.

#### Macports

Now we can install the [Macports](https://www.macports.org) package manager. Download the
corresponding `pkg` file and run the installation.

This adds the following lines to the `.bash_profile` file:

```
# MacPorts Installer addition on 2021-12-22_at_17:39:58: adding an appropriate PATH variable for use with MacPorts.
export PATH="/opt/local/bin:/opt/local/sbin:$PATH"
# Finished adapting your PATH environment variable for use with MacPorts.
```

These lines could be removed and added to the `$PATH` declaration in `.bashrc`.

#### Python

See specific section.

Installing the PSF Python adds the following lines to `.bash_profile`:

```
# Setting PATH for Python 3.10
# The original version is saved in .bash_profile.pysave
PATH="/Library/Frameworks/Python.framework/Versions/3.10/bin:${PATH}"
export PATH
```
The resulting `$PATH` looks like:

    /Library/Frameworks/Python.framework/Versions/3.10/bin:/opt/local/bin:/opt/local/sbin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/opt/X11/bin:/Library/Apple/usr/bin

Installing the Anaconda Python distribution adds the following lines to `.bash_profile`

```
# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/Users/antonio/opt/anaconda3/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "/Users/antonio/opt/anaconda3/etc/profile.d/conda.sh" ]; then
        . "/Users/antonio/opt/anaconda3/etc/profile.d/conda.sh"
    else
        export PATH="/Users/antonio/opt/anaconda3/bin:$PATH"
    fi
fi
unset __conda_setup
# <<< conda initialize <<<
```

And sets the `$PATH` variable to:

    /Users/antonio/opt/anaconda3/bin:/Users/antonio/opt/anaconda3/condabin:/Library/Frameworks/Python.framework/Versions/3.10/bin:/opt/local/bin:/opt/local/sbin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/opt/X11/bin:/Library/Apple/usr/bin

However, this initializes the **conda** `base` environment for each new shell opened. To prevent this:

    $ conda config --set auto_activate_base false

This creates a file `.condarc` with the following content:

    auto_activate_base: false

Now when opening a new shell the **conda** `base` environment is not activated, and the
`$PATH` variable is set to:

    /Users/antonio/opt/anaconda3/condabin:/Library/Frameworks/Python.framework/Versions/3.10/bin:/opt/local/bin:/opt/local/sbin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/opt/X11/bin:/Library/Apple/usr/bin

This means that the PSF Python takes preference over the Anaconda Python. To change this,
simply activate a **conda** environment:

    $ conda activate         # activates the base environment
    $ conda activate seismo  # activates the "seismo" environment


