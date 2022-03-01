# MacPorts

https://www.macports.org

    $ sudo port [-v] selfupdate       # -v for verbose
    $ sudo port upgrade outdated      # this can take a long time
    $ sudo port rev-upgrade           # if something goes wrong

Other macports commands:

    $ port version
    $ port installed
    $ port search --name --glob "gmt*"
    $ port search --name --line --glob "gmt*" # produces better output

    $ port info gmt5

## System tools

- `wget`
- `curl`
- `htop`
- `tree`
- `exa`: a modern replacement for `ls`
- `bat`: a `cat` clone written in `Rust`
- `openssh`
- `coreutils`
- `inetutils`: ftp, telnet
- `tmux`
- a more modern `bash`: currently 5.1.16 (versus 3.2 system `bash`)

```
$ sudo port install openssh +ssh-copy-id
```

## Development

Some of the tools install (multiple versions of) programming languages,
such as `C/C++`, `Python`, `Perl`, `Rust`, etc.

Normally those installations are only used by MacPorts to build some of its
applications and packages. However they can also be used for development.
For example, to make the `MacPort`'s Python the default Python:

```
python39 has the following notes:
 To make this the default Python or Python 3 (i.e., the version run by the 'python' or 'python3' commands), run one or both of:

      sudo port select --set python python39
      sudo port select --set python3 python39
```

In addition to those languages, the following development tools can
also be installed:

- `cmake`
- `gsl`: GNU Scientific Library
- [`graphviz`]: graph visualization software
- [`gnuplot`]: command-line graphing utility
- `gh`: GitHub command-line tools
- `pipx`
- `openmpi`

```
  openmpi-default has the following notes:
    The mpicc wrapper (and friends) are installed as:
      /opt/local/bin/mpicc-openmpi-mp (likewise mpicxx, ...)

    To make openmpi-default's wrappers the default (what you get when you execute 'mpicc' etc.) please run:
      sudo port select --set mpi openmpi-mp-fortran

```

Some packages install versions of Python. To make those versions the default Python/Python3:


## Utilities

- `a2ps`
- `gv`
- `ffmpeg`
- `graphicsmagick`
- [`feh` not installed in Monterrey; gives error]
- `latexdiff`

```
sudo port install ffmpeg +libgfortran3 +openmpi
```
## Packages

- `gmt6`

```
$ sudo port install gdal +hdf5 +netcdf +openjpeg
$ sudo port install gmt6 +fftw3
```
