# MacPorts

https://www.macports.org

    $ sudo port [-v] selfupdate [verbose]
    $ sudo port upgrade outdated
    $ sudo port rev-upgrade [if something goes wrong]

Other macports commands:

    $ port version
    $ port installed
    $ port search --name --glob "gmt*"
    $ port search --name --line --glob "gmt*" [better output]

    $ port info gmt5

Installed ports:
===============

- a2ps
- coreutils
- feh
- ffmepg
- gmt6 (gdal, gshhg-gmt, netcdf)
- gv
- GraphicsMagick
- htop
- inetutils
- openmpi
- openssh
- tmux
- wget


```console
$ sudo port install gv
$ sudo port install wget
$ sudo port install curl
$ sudo port install coreutils

[ Installation instructions for GMT 6:
https://github.com/GenericMappingTools/gmt/blob/master/INSTALL.md ]

$ sudo port install gdal +hdf5 +netcdf +openjpeg  [ + indicates a variant ]
$ sudo port install gmt6 [ +fftw3 +openmp ]

$ sudo port install ImageMagick
$ sudo port install GraphicsMagick [ same as graphicsmagick? ]
$ sudo port install ffmpeg

$ sudo port install a2ps
$ sudo port install feh

$ sudo port install openfortivpn
$ sudo port install openssh +ssh-copy-id
$ sudo port install inetutils (ftp, telnet)

$ sudo port install tmux
$ sudo port install htop

$ sudo port install cmake

[ openmpi ?]

To install camfort (finally did not work)

$ sudo port install gsl
$ sudo port install z3
$ sudo port install flint
$ sudo port install cabal
```



```
gv:

  libidn has the following notes:
    Please be aware that GNU libidn2 is the successor of GNU libidn. It comes with IDNA 2008
    and TR46 implementations and also provides a compatibility layer for GNU libidn.

openssh:

  openssh has the following notes:
    Apple's keychain integration and launchd changes are now included by default, not just with the gsskex variant.
    The parameters were changed from -m/-M to -A/-K in accordance with Apple's changes, because upstream started using the former switches themselves recently.

    A startup item has been generated that will aid in starting openssh with launchd. It is disabled by default. Execute the following command to start it, and to cause it to launch at startup:

        sudo port load openssh


wget:

  libpsl has the following notes:
    libpsl API documentation is provided by the port 'libpsl-docs'.
  wget has the following notes:
    To customize wget, you can copy /opt/local/etc/wgetrc.sample to /opt/local/etc/wgetrc and then make changes.

gdal:

  bash-completion has the following notes:
    To use bash_completion, add the following lines at the end of your .bash_profile:
      if [ -f /opt/local/etc/profile.d/bash_completion.sh ]; then
          . /opt/local/etc/profile.d/bash_completion.sh
      fi

    The port bash-completion >=2.0 requires bash >=4.1; please make sure
    you are using /opt/local/bin/bash by changing the preferences of your
    terminal accordingly. If your version of bash is too old, the script
    above will not modify your shell environment and no extended completion
    will be available.
  hdf5 has the following notes:
    Mac users may need to set the environment variable "HDF5_USE_FILE_LOCKING" to the five-character string "FALSE" when accessing network mounted files.  This is an application run-time setting, not a configure or build
    setting.  Otherwise errors such as "unable to open file" or "HDF5 error" may be  encountered.
  netcdf has the following notes:
    As of version 4.2 c++ and fortran interfaces are separate ports, netcdf-cxx and netcdf-fortran, respectively.

coreutils:

  coreutils has the following notes:
    The tools provided by GNU coreutils are prefixed with the character 'g' by default to distinguish them from the BSD commands.
    For example, cp becomes gcp and ls becomes gls.

    If you want to use the GNU tools by default, add this directory to the front of your PATH environment variable:
        /opt/local/libexec/gnubin/

ImageMagick:

  python37 has the following notes:
    To make this the default Python or Python 3 (i.e., the version run by the 'python' or 'python3' commands), run one or both of:

        sudo port select --set python python37
        sudo port select --set python3 python37


ffmpeg:

  ffmpeg has the following notes:
    *******
    ******* This build of ffmpeg includes GPLed code and
    ******* is therefore licensed under GPL v2 or later.
    *******
    ******* The following modules are GPLed:
    *******
    *******      postproc
    *******      libx264
    *******      libx265
    *******      libxvid
    *******
    ******* To include all nonfree, GPLed and LGPL code use variant +nonfree.
    ******* To remove nonfree and GPLed code leaving only LGPL code remove the
    ******* +gpl2 variant.
    *******
  python27 has the following notes:
    To make this the default Python or Python 2 (i.e., the version run by the 'python' or 'python2' commands), run one or both of:

        sudo port select --set python python27
        sudo port select --set python2 python27

openssh:

  openssh has the following notes:
    Apple's keychain integration and launchd changes are now included by default, not just with the gsskex variant.
    The parameters were changed from -m/-M to -A/-K in accordance with Apple's changes, because upstream started using the former switches themselves
    recently.

    A startup item has been generated that will aid in starting openssh with launchd. It is disabled by default. Execute the following command to start it,
    and to cause it to launch at startup:

        sudo port load openssh

inetutils:

  inetutils has the following notes:
    All clients are now installed with the "g" prefix.

tmux:

    If you want integration with system pasteboard consider installing port tmux-pasteboard as well

openmpi:

--->  Some of the ports you installed have notes:
  openmpi-default has the following notes:
    The mpicc wrapper (and friends) are installed as:

      /opt/local/bin/mpicc-openmpi-mp (likewise mpicxx, ...)

    To make openmpi-default's wrappers the default (what you get when
    you execute 'mpicc' etc.) please run:

      sudo port select --set mpi openmpi-mp-fortran

OpenCoarrays:

failed!!

$ sudo port clean OpenCoarrays

$ sudo port install graphviz

$ sudo port install openmpi

--->  Some of the ports you installed have notes:
  openmpi-default has the following notes:
    The mpicc wrapper (and friends) are installed as:

      /opt/local/bin/mpicc-openmpi-mp (likewise mpicxx, ...)

    To make openmpi-default's wrappers the default (what you get when
    you execute 'mpicc' etc.) please run:

      sudo port select --set mpi openmpi-mp-fortran
```




