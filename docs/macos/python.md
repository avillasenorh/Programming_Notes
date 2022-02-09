## Python installation

![xkcd Python environment](https://imgs.xkcd.com/comics/python_environment.png)

Initially an old system version of Python is installed:

```
$ /usr/bin/python -V
Python 2.7.18

$ /usr/bin/python

WARNING: Python 2.7 is not recommended.
This version is included in macOS for compatibility with legacy software.
Future versions of macOS will not include Python 2.7.
Instead, it is recommended that you transition to using 'python3' from within Terminal.

Python 2.7.18 (default, Jan  4 2022, 17:47:56)
[GCC Apple LLVM 13.0.0 (clang-1300.0.29.10) [+internal-os, ptrauth-isa=deployme on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

This is in fact a link to:

    /usr/bin/python@ -> ../../System/Library/Frameworks/Python.framework/Versions/2.7/bin/python2.7

As stated in the warning, it is expected that macOS Monterrey Version 12.3 (early 2022)
will not include this Python 2.7 distribution.

There is no `pip` command associated with this version of Python.

In `/usr/bin` there is also a newer version of Python:

```
$ /usr/bin/python3 -V
Python 3.8.9

$ /usr/bin/python3
Python 3.8.9 (default, Oct 26 2021, 07:25:54)
[Clang 13.0.0 (clang-1300.0.29.30)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

There is a `pip3` command associated with this version of Python:

```
$ /usr/bin/pip3 -V
pip 20.2.3 from /Applications/Xcode.app/Contents/Developer/Library/Frameworks/Python3.framework/Versions/3.8/lib/python3.8/site-packages/pip (python 3.8)
```

However none of these versions should be used (only used by operating systems) and do not
install packages!

Therefore we need to install other distributions of Python.

### PSF Python

In addition to system python (not used) the first Python distribution to install
is that of the [PSF](https://www.python.org). For macOS we select a
macOS 64-bit universal2 installer (`.dmg` file).

The installation is simple, but it requires a set of SSL root certificates:

![install Python certificates](python_certificates.png)

When clicking in the `Install Certificates` icon:

```

$ ./Install\ Certificates.command
 -- pip install --upgrade certifi
Collecting certifi
  Downloading certifi-2021.10.8-py2.py3-none-any.whl (149 kB)
     |████████████████████████████████| 149 kB 4.2 MB/s
Installing collected packages: certifi
Successfully installed certifi-2021.10.8
WARNING: You are using pip version 21.2.4; however, version 21.3.1 is available.
You should consider upgrading via the '/Library/Frameworks/Python.framework/Versions/3.10/bin/python3.10 -m pip install --upgrade pip' command.
 -- removing any existing file or link
 -- creating symlink to certifi certificate bundle
 -- setting permissions
 -- update complete

```

The PSF installation adds the following lines to your `.bash_profile`:

```
# Setting PATH for Python 3.10
# The original version is saved in .bash_profile.pysave
PATH="/Library/Frameworks/Python.framework/Versions/3.10/bin:${PATH}"
export PATH
```

The resulting `$PATH` variable looks like:

```
/Library/Frameworks/Python.framework/Versions/3.10/bin:/opt/local/bin:/opt/local/sbin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/opt/X11/bin:/Library/Apple/usr/bin
```

And now we have:

```
$ command -v python3
/Library/Frameworks/Python.framework/Versions/3.10/bin/python3

$ python3
Python 3.10.1 (v3.10.1:2cd268a3a9, Dec  6 2021, 14:28:59) [Clang 13.0.0 (clang-1300.0.29.3)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

WARNING: the `python` command still points to the 2.7 version, so we have to use `python3`

### Upgrade pip/pip3

When installing the SSL root certificates we obtained a warning that
a newer version of `pip` is available. To install this new version:
```
$ command -v pip3
/Library/Frameworks/Python.framework/Versions/3.10/bin/pip3

$ command -v python3
/Library/Frameworks/Python.framework/Versions/3.10/bin/python3

$ pip3 --version
pip 21.2.4 from /Library/Frameworks/Python.framework/Versions/3.10/lib/python3.10/site-packages/pip (python 3.10)

$ ls -l /Library/Frameworks/Python.framework/Versions/3.10/bin/pip3
pip3     pip3.10

$ ls -l /Library/Frameworks/Python.framework/Versions/3.10/bin/pip3
-rwxrwxr-x  1 root  admin   270B Dec 22 17:48 /Library/Frameworks/Python.framework/Versions/3.10/bin/pip3*

$ /Library/Frameworks/Python.framework/Versions/3.10/bin/python3.10 -m pip install --upgrade pip
Requirement already satisfied: pip in /Library/Frameworks/Python.framework/Versions/3.10/lib/python3.10/site-packages (21.2.4)
Collecting pip
  Downloading pip-21.3.1-py3-none-any.whl (1.7 MB)
     |████████████████████████████████| 1.7 MB 1.8 MB/s
Installing collected packages: pip
  Attempting uninstall: pip
    Found existing installation: pip 21.2.4
    Uninstalling pip-21.2.4:
      Successfully uninstalled pip-21.2.4
Successfully installed pip-21.3.1

$ ls -l /Library/Frameworks/Python.framework/Versions/3.10/bin/pip3
-rwxr-xr-x  1 antonio  admin   270B Dec 22 18:15 /Library/Frameworks/Python.framework/Versions/3.10/bin/pip3*

$ ls -l /Library/Frameworks/Python.framework/Versions/3.10/bin/pip*
-rwxr-xr-x  1 antonio  admin   270B Dec 22 18:15 /Library/Frameworks/Python.framework/Versions/3.10/bin/pip*
-rwxr-xr-x  1 antonio  admin   270B Dec 22 18:15 /Library/Frameworks/Python.framework/Versions/3.10/bin/pip3*
-rwxr-xr-x  1 antonio  admin   270B Dec 22 18:15 /Library/Frameworks/Python.framework/Versions/3.10/bin/pip3.10*

$ pip3 --version
pip 21.3.1 from /Library/Frameworks/Python.framework/Versions/3.10/lib/python3.10/site-packages/pip (python 3.10)

$ pip --version
pip 21.3.1 from /Library/Frameworks/Python.framework/Versions/3.10/lib/python3.10/site-packages/pip (python 3.10)
```

Now we have:

```
$ command -v pip
/Library/Frameworks/Python.framework/Versions/3.10/bin/pip

$ command -v pip3
/Library/Frameworks/Python.framework/Versions/3.10/bin/pip3
```

### Install Anaconda

Adds to `.bash_profile`:


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

Path now looks like:

```
/Users/antonio/opt/anaconda3/bin:/Users/antonio/opt/anaconda3/condabin:/Library/Frameworks/Python.framework/Versions/3.10/bin:/opt/local/bin:/opt/local/sbin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/opt/X11/bin:/Library/Apple/usr/bin
```

To prevent the activation of the base environment:

    $ conda config --set auto_activate_base false

This creates a file .condarc with the following content:

    auto_activate_base: false


Now, when opening a new shell `$PATH` is:

```
/Users/antonio/opt/anaconda3/condabin:/Library/Frameworks/Python.framework/Versions/3.10/bin:/opt/local/bin:/opt/local/sbin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/opt/X11/bin:/Library/Apple/usr/bin
```

### Install packages with pipx

```
$ sudo port install pipx

$ pipx install black
  installed package black 21.12b0, installed using Python 3.9.9
  These apps are now globally available
    - black
    - black-primer
    - blackd
⚠️  Note: '/Users/antonio/.local/bin' is not on your PATH environment variable. These apps will not be globally accessible until your PATH is updated. Run
    `pipx ensurepath` to automatically add it, or manually modify your PATH in your shell's config file (i.e. ~/.bashrc).
done! ✨ 🌟 ✨
```

Modify `.bashrc` to add `/Users/antonio/.local/bin`


