# ObsPy

Notes on using ObsPy

## Installation and updates of conda, pip, etc

    $ conda update conda
    $ conda update anaconda

    $ pip install --upgrade pip

## Installation of ObsPy

Suggested approach, using an environment for obspy

    $ conda create -n obspy python=3.5 anaconda
    $ source activate obspy
    $ (obspy) conda install -c conda-forge obspy
    $ (obspy) conda update -c conda-forge obspy
    $ (obspy) obspy-runtests 


Another approach, adding conda-forge to list of channels 

    $ conda config --add channels conda-forge
    $ conda config --add channels obspy
    $ conda install obspy
    $ conda update obspy
    $ obspy-runtests

Other packages installed (using conda, pip, or others)

    $ pip install eqcorrscan

Other packages to install

To fix this error while running obspy-runtests:


OSError: Unable to open boundary dataset file. Only the 'crude' and  'low',
resolution datasets are installed by default.
If you are requesting an, 'intermediate', 'high' or 'full'
resolution dataset, you may need to download and install those
files separately with
`conda install -c conda-forge basemap-data-hires`.

$ conda install -c conda-forge mtspec
The following NEW packages will be INSTALLED:

    libgfortran: 3.0.0-0      conda-forge
    mtspec:      0.3.2-py35_1 conda-forge


Other packages installed in obspy environment:

    $ cd LOKI-LOCATOR
    $ mk_anaconda.sh
    $ python installation.py install

    $ cd LatLongUTMconversion_python3/
    $ python setup.py install

## Check if file/directory exists

```python
import os
os.path.isfile("file")                      # True for regular file, False for directory!
os.path.isdir("directory")
os.path.exists("file_or_directory")         # True for existing file or directory
```

## Write to stdout and stderr

```python
sys.stdout.write("message\n")
sys.stderr.write("error\n")
```

## Read a text file in Python (see Python Cookbook, page 141)

Read the entire file as a single string

```python
with open('somefile.txt', 'rt') as f:
    data = f.read()
```

Iterate over the lines of the file

```python
with open('somefile.txt', 'rt') as f:
    for line in f:
```

- to split line in columns:

```python
columns = line.split()
```

## Formatted print

Comprehensive documentation and examples in:
https://pyformat.info

```python
print('format string'.format(variable1, variable2, variable3, ...))

example of format string:

print('{0:6} {1:03d} {2:07.4f}'.format('PAB', 5, 3.4))
PAB    005 03.4000
```


## Run an external command in Python

```python
import subprocess

subprocess.call('ls')

subprocess.call(['ls', '-l']) -> writes to stdout

output_str = subprocess.check_output(['ls', '-l']) -> writes to string "output_str"
```

Options of subprocess.call:
    stdin=None   -> redirects input from a file or an open pipe
    stdout=None  -> redirects output to a file
    stderr=None
    shell=False  -> sends command to the UNIX shell (to use shell shortcuts and optimizations, e.g. wildcards)
                    then string is only one: 'ls *.py'

## Making day plots

```python
from obspy import read
from obspy.core import UTCDateTime  (if you are going to operate with time strings)

st = read("DD.D006..HHZ.D.2016.234")
st.plot(type="dayplot", outfile="DD.D006..HHZ.D.2016.234.raw.png")

st.filter("bandpass", freqmin=3, freqmax=15, corners=3)
st.plot(type="dayplot", outfile="DD.D006..HHZ.D.2016.235.filtered.png")


st.plot(type="dayplot", outfile="DD.D044..HHZ.D.2016.267.filtered.png",
starttime=UTCDateTime("2016-09-23T07:00:00.0Z"),					# set start time (exclude installation)
show_y_UTC_label=False,								# eliminate ugly "local time" label
size=(2000,1200),								# doubles the size of "dayplot" plot
vertical_scaling_range=5.0E2)							# clip largest signal
```

More options in:
http://docs.obspy.org/packages/autogen/obspy.core.stream.Stream.plot.html#obspy.core.stream.Stream.plot


## Checking for data availability using obspy-scan

    $ obspy-scan path = scan contents of all  files in directory "path" and generates an interactive plot

    $ obspy-scan --no-x 2016/DD/*/*Z.D

- produces an interactive plot only for vertical components
- does not plot an x for the start time of each data file


    $ obspy-scan --no-x --print-gaps -o 2016.pdf 2016 > 2016.gaps

- produces a pdf file instead of an interactive plot
- writes gaps to stdout
- does not plot an x for the start time of each data file
