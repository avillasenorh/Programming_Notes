# SEISAN

## SEISAN directories

```
COM		Shell and bat scripts to define variables
INC		Include files
INF		Documentation (pdf files)
ISO		?? (macro files)
LIB		Libraries (and its source code)
PIC		Pictures (used?)
PRO		Executables and source code
SUP		Supplementary programs (dataselect and SE)
TMP		empty

CAL		Instrument responses
DAT		Parameter files
REA		Phase data
WAV		Waveform data

WOR
```

## SEISAN installation on Linux

SEISAN 10.5 Installation on xlr8 (Ubuntu 16.04 LTS)

1. Edit SEISAN.bash and add it to .bashrc

```
$ source .bashrc # for changes to take place
```

2. Compile libraries

```
$ cd $SEISAN_TOP
$ cd LIB
$ make clean
$ make all > make.log 2>&1
```

3. Compile programs

```
$ pr
$ make clean
$ make all > make.log 2>&1
```

4. Re-create IASP91 tables

```
$ wo
$ remodl
$ setbrn
$ cp IASP91_linux.* ../DAT/.
```

5. Run test events

```
$ eev 199606 
```

## Installation of SEISAN 10.0 in Linux


1. Edit /data/seismo/COM/SEISAN.csh

SEISAN_TOP

comment PITSA variables
comment LD_LIBRARY_PATH
comment path (add $SEISAN_TOP/PRO in .cshrc)

2. Go to $SEISAN_TOP/LIB and edit Makefile

Eliminate  -fbounds-check option

```
fc_gfortran  = gfortran -g -c -I../INC -fdollar-ok -fno-automatic -o $@
#fc_gfortran  = gfortran -g -c -I../INC -fdollar-ok -fbounds-check -fno-automatic -o $@
```

% make clean

3. Go to $SEISAN_TOP/PRO and edit Makefile

Eliminate  -fbounds-check option

```
fc_gfortran = gfortran -g -I../INC -fdollar-ok -fno-automatic -o $@
#fc_gfortran = gfortran -g -I../INC -fdollar-ok -fbounds-check -fno-automatic -o $@
```

Change INSTALL_PRO_PATH (needed?)
INSTALL_PRO_PATH = /data/seismo/PRO

% make clean
% make all >&! log &
% tail -f log


4. Install Seisan Explorer

Install qt4-make qt4-dev-tools with Synaptic

% cp $SEISAN_TOP/LIB/seisan.a linux/.

% qmake se.pro (creates Makefile)

% make >&! log &
[does not work!!]

## SEISAN for Dehdasht

SEISAN for processing DehDasth data

1. Set continuous data in arclink directory structure

2. Get station coordinates and format them in HYP format:

```
  D0063045.23N 5028.63E   0   (not processed!!!)
  D0293043.69N 5033.91E 754
  D0493047.22N 5032.94E 828
  D0553042.69N 5038.32E 848
  D0693053.64N 5029.77E 963
  D0733050.46N 5033.17E 905
  D0783046.53N 5037.44E 806
  D0813044.18N 5040.46E 814
  D0913047.31N 5038.41E 847
  D0953055.27N 5031.62E 875
  D0983052.78N 5034.19E 941
  D1043048.01N 5039.30E 852
  D1073045.66N 5041.85E 827
```

3. Edit configuration files STATION0.HYP, SEISAN.DEF, MULPLT.DEF

IMPORTANT!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

When editing SEISAN.DEF and MULPLT.DEF use **FLOATING POINT** values, **NO** integer values.
Most of the errors are caused by using integer values instead of floating point values.
If something does not work, check this first!!!
Write values starting at column 41


3.1. STATION0.HYP

change station list

change 1D velocity model (once one is available)

3.2. SEISAN.DEF

Define the location of the arclink directory and all the stations/channels

```
ARC_ARCHIVE                             /scratch/DehDasht
ARC_CHAN                                D006 HHEDD
ARC_CHAN                                D006 HHNDD
ARC_CHAN                                D006 HHZDD
ARC_CHAN                                D029 HHEDD
...
ARC_DURATION                            300.0
```

Set cursor to cross-hair:

```
CURSOR             0: default, 1: cross 2.
```

Set map default dimensions and plot stations

```
MAP_LAT_BORDER     dist from center       2.0
MAP_LON_BORDER          "                 2.0
EPIMAP_STATIONS    plot stations        1.
```


3.3. MULPLT.DEF

Set keys for assigning weights (depends on keyboard!!!)

```
PHASE WEIGHT KEY                        =         0
PHASE WEIGHT KEY                        !         1
PHASE WEIGHT KEY                        "         2
PHASE WEIGHT KEY                        %         3
PHASE WEIGHT KEY                        $         4
```

(weight 3 assigned pressing SHIFT + 5 !!!)

Sort seismograms by distance:

```
NSORT_DISTANCE     0: no sort, min ph.  1.
```


Change number of channels per screen when doing manual picking

```
NCHAN PER SCREEN   # chan pr screen     3.
```


4. Visually inspect continuous data

First un-comment `NCHAN PER SCREEN` in `MULPLT.DEF`


```console
$ mulplt
  Filename, number, filenr.lis (all)
  Continuous SEISAN data base: cont
  Large SEED volume: conts
  Archive: arc
  Make a choice
arc
 Give start time, yyyymmddhhmmss
20160822
 Interval in min
15

[ select ALL with cursor ]

  Plot options: Interactive picking          Return
                Multi trace plot on screen, def (0)
                Multi trace plot on screen      (1)
                Multi trace plot on screen+laser(2)
                Multi trace plot on laser       (3)
                Continuoues on screen           (4)
                Continuoues on screen + laser   (5)
                Continuoues on laser            (6)
                Stop                            (q)
0
  Low and high cut for filter, return for no filter
3 15

[ press "f" no move to next screen; click to zoom; "p" to save segment ]


 ENTER EVENT TYPE L,R OR D
 Second. optional character for event ID (e.g. E)
 Third optional character for model ID (e.g. J) L
  Give operator code (max 4 char)
avh
  Give 2-5 letter data base, ,, for local dir, return for default base
,,
 Output channels on screen: s
 No output, just register:  n
 No output, just ARC line:  a
 Output all channels:   enter

a

 S-file name:   22-0100-10L.S201608
 GO AHEAD (Y/N)
y

  Continue plot(y/n=default)
y
```

Other parameters

    GMAP_ICON_MSIZE                         3.0 (so events with M=0 are visible)




