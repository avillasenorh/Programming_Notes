UNIX tips and commands
======================

"The Enlightened Ones say that. . .

- You should never use C if you can do it with a script;
- You should never use a script if you can do it with awk;
- Never use awk if you can do it with sed;
- Never use sed if you can do it with grep.“

    $ man hier (Unix directory structure)

    $ compgen -b 

Lists built-in commands. See also:

    $ man builtin

## Command-line shortcuts

`Ctrl-u` to delete current command,<br>
`Ctrl-l` to "clear" output<br>
`Ctrl+r` : Backward search<br>
`Ctrl+s` : Pause output<br>
`Ctrl+q` : Resume output after Ctrl+s<br>
`Ctrl+a` : move to the BOL<br>
`Ctrl+e` : move to the EOL<br>
`Ctrl+k` : delete all text from the cursor to EOL<br>
`Ctrl+_` : undo<br>

Move:

`Ctrl + A`      -> beginning of line<br>
`Alt  + B`      -> beginning of word<br>
`Ctrl + B`      -> previous character<br>

`Ctrl + F`      -> next character<br>
`Alt  + F`      -> end of word<br>
`Ctrl + E`      -> end of line<br>

Delete:

`Ctrl + U`      -> to beginning of line<br>
`Ctrl + W`      -> to beginning of word<br>

`Alt  + D`      -> to end of word<br>
`Ctrl + K`      -> to end of line<br>

(Alt shortcuts do not work on iTerm2)

open long and complicated Linux or Unix commands in a text editor. Press:

`Ctrl + x` `Ctrl + e`

## Arguments

`!^` is the first argument of the previous command
`!$` is the last argument of the previous command

## Prompt

Show terminal colors:

    $ printf "\e[%dm%d dark\e[0m \e[%d;1m%d bold\e[0m\n" {30..37}{,,,}

## pwd

    $ pwd -L		# logical (e.g. soft link)
    $ pwd -P		# physical

## type

```
$ type ls
ls is aliased to `ls -GFh'
$ type cd
cd is a shell builtin

$ type -a ls
ls is aliased to `ls -GFh'
ls is /bin/ls
```

## which

## compgen

    $ compgen -c   # lists all available command, aliases, ...

## stat

```console
$ stat -x gmt.conf
  File: "gmt.conf"
  Size: 3192         FileType: Regular File
  Mode: (0644/-rw-r--r--)         Uid: (  501/ antonio)  Gid: (   20/   staff)
Device: 1,8   Inode: 16647540    Links: 1
Access: Thu Sep 15 10:12:53 2016
Modify: Mon Jun  8 14:45:18 2015
Change: Mon Jun  8 14:45:18 2015
```

## file

```console
$ file gmt.conf
gmt.conf: ASCII text
$ file -b gmt.conf
ASCII text
```

## ls

To expand a wildcard whithout doing an "ls"

    $ echo .*
    $ echo .[!.]*

To list the files in another directory that match more than one pattern:

    $ ls -l /etc/{*.conf,*.rc,*.sh}

List all directories starting with an uppercase letter:

    $ ls -1d [[:upper:]]*

To rename all `*.bak` to `*.txt` on a Linux/Unix/OSX (bash shell)

    $ for j in *.bak; do mv -v -- "$j" "${j%.bak}.txt"; done

Quick comparing of 2 dirs:

    $ diff -y <(ls -l ${DIR1}) <(ls -l ${DIR2})

Alternative:

    $ diff --brief --recursive dir1 dir2

Enter special characthers (such as ^G = bell)

press ctrl-v and then special character (e.g. ctrl-G)


Define a variable and run a script.
The variable is only used inside the script

    $ MYVAR=value ./script.sh

## eval

use eval to define environmental variables:

    $ eval $( command_that_generates_variables) [not tested] 

Print a variable between quotation marks:
These 3 commands produce the same output:

```
$ echo "SACAUX is "\"$SACAUX\"
$ echo SACAUX is \"$SACAUX\"
$ echo "SACAUX is \"$SACAUX\""
SACAUX is "/usr/local/sac/lib/aux"
```

## xdg-opeon

`xdg-open` will open a file from the command line using the application associated with its file extension.

## tar

First see structure of tar file with

    $ tar tvzf latest.tar.gz | more

    $ tar xvzf latest.tar.gz -C /directory/ --strip=1 # eliminates first directory from tar

## rsync

    $ rsync -avc orig dest

To check only: (I have not tried this!!!)

    $ rsync -niaHc /origfolder/ /copyfolder   ( "/" after origfolder is important!!!)

```
-n do not copy ("dry run")
-i itemise the differences
-a preserve (i.e. compare since we have -n) permissions, ownerships, symbolic links, etc. and recurse down directories
-H preserve hard links
-c compare checksums
```

Reproduce a directory structure but without copying files

    $ rsync -av -f"+ */" -f"- *" "$source" "$target"

## a2ps

    $ a2ps -R --font-size=8 --columns=1 -M A4 README.txt

-o ouput.ps            -> writes output to a PostScript file
-P printer             -> send to an specified printer
-P display             -> send to gv (does not work in MacOS X)
-M Letter

## sort, uniq

Show which lines are repeated in a sorted file:

    $ uniq -d sorted_file

Find duplicated lines

    $ sort file | uniq -d

## find

    $ find .          # find all files hanging from .
    $ find . -print   # same

    $ find . ! -name "*.txt" -print               # find files that do not match pattern

    $ find .  -name "*${str}*" -printf '%P\n'     # get rid of annoying "./" (not for MacOS X :-(

    $ find .  -name "*${str}*" -print | cut -c3-  # trick to do the same by starting at 3rd character

    $ find . \( -name "*.txt" -o -name "*.pdf" \) -print   # use OR (-o)

-path looks for matches in full path, while -name only in file name
-maxdepth -mindepth specify directory depth

-type  : f = file, d = directory, l = link, ...

-atime : access time
-mtime : modification time (content)
-ctime : change time (metadata: permissions, ownership)

    $ find . -type f -atime -7 -print   # files accessed WITHIN the last 7 days
    $ find . -type f -atime  7 -print   # files accessed EXACTLY 7 days ago 
    $ find . -type f -atime +7 -print   # files accessed EARLIER than 7 days ago

-amin, -mmin, -cmin : same but in minutes

    $ find . -type f -newer file.txt -print   # finds file.txt with earliest modification time

    $ find . -type f -size +2k       # Files having size greater than 2 kilobytes
    $ find . -type f -size -2k       # Files having size less than 2 kilobytes
    $ find . -type f -size 2k        # Files having size 2 kilobytes

can also use k, M, G

    $ find . -type f -perm 644 -print  # can be useful to change permissions of miniSEED files in arclink structure
    $ find . -type f -name "*.php" ! -perm 644 -print  # this one too
    $ find . -type f -user iber -print

- Executing commands and actions with find!!!!

    $ find . -type f -name "*.SAC" -exec /bin/rm -f {} \;

    $ find . -type f -user root -exec chown iber {} \; # runs a chown command for each file
    $ find . -type f -user root -exec chown iber {} \+ # runs a single chown command for all files 

    $ find . -type f -name "*.c" -exec cat {} \;>all_c_files.txt # concatenate all C files in a single file (note >, not >> !!)

    $ find . -type f -mtime +10 -name "*.txt" -exec cp {} OLD  \;
    $ find . -type f -name "*.txt" -exec printf "Text file: %s\n" {} \;

    $ find devel/source_path  \( -name ".git" -prune \) -o \( -type f -print\) # ignore directory .git

    $ find / -type f -printf '%T+ %p\n' | sort | head -n 1   # Find oldest file in your filesystem

-maxdepth 1 : does not go into subdirectories

The find action -printf '%P\n' prints the name without the starting directory,
meaning no ./ is present to need to be stripped.

    $ find . -maxdepth 1 -type d -name "[012]???" -printf "%P\n"              # does not work in macOS
    $ find . -maxdepth 1 -type d -name "[012]???" -print | sed "s|^\./||"     # works everywhere
    $ find . -maxdepth 1 -type d -name "[012]???" -print | cut -c3-

    $ find * -maxdepth 0 -type d -name "[012]???" -print                      # this also works!!!! but maxdepth is 0!!!


- Find empty directories and remove then:
    $ find . -type d -empty -delete

- Consolidate ("flatten") all subdirectories in one directory

    $ find TargetDirectory/ -mindepth 2 -type f -exec mv -i '{}' TargetDirectory/ ';'


## cut

    $ echo a:b:c | cut -d: -f1

## tr

    $ tr '\r' '\n' < mac-format-file.txt      # fix carriage return problem for files created with GUI Mac applications 

## nl

Numbers lines in a text file

## csplit 

splits file in parts using matching patterns

    $ csplit -k -s -n 4 $QAFI '/^>/' '/^>/' "{1000}"

```
-k : do not remove output files if an error occurs
-n : number of digits in output xx* files
-s : do not output to stdout the number of lines of each file
```

# Human readable path:

    $ echo "${PATH//:/$'\n'}"

In order to write this as an alias, replace `'` with `'"'"'`:

    alias human_path='echo "${PATH//:/$'"'"'\n'"'"'}"'

## ed

Addresses
i       : line i
$       : last line
1,$ = % : all lines in file
i,j     : lines i through j
.       : current line

Commands

:0r $HOME/data             : read file in at top of current file
:g/Name:/s/tom/Tom/        : substitute tom for Tom in lines that match /Name:/
:1,10s/yes/no/g            : Substitute on first 10 lines
:%s/[Hh]ello/Hi/gc         : Confirm global substitutions
:s/Fortran/\U&/ 3          : Confirm global substitutions Uppercase “Fortran” on next 3 lines


ed map.sh << EOF
g/^ps/s//gmt &/p
g/10 0 1 LB/s///p
/pstext/
s:G0/0/0:G255 -F+f10p,Helvetica+jLB:p
w
q
EOF

## grep-awk

Use `pgrep` instead of `grep`

Equivalent `grep´ and `awk` commands for pattern matching:

    $ grep a input | grep b | grep -v c | grep d
    $awk '/a/ && /b/ && !/c/ && /d/' input


Print every 10th line from a file:

    $ awk '!(NR % 10)' file



## camel case and underscore

    $ echo "hello_world" | sed -r 's/([a-z]+)_([a-z])([a-z]+)/\1\U\2\L\3/'
    $ echo thisIsATest | sed -r 's/([A-Z])/_\L\1/g'

## ssh-related commands

    $ sudo port install openssh +ssh-copy-id

    $ ssh-keygen -b 4096 -t rsa


To install key in another server:

    $ ssh-copy-id -i ~/.ssh/id_rsa.pub antonio@xlr8.ictja.csic.es [will ask for password]

## Terminal multiplexers

Keep your terminal sessions alive and well under `Linux/*BSD/macOS` and Unix-like systems.

1. screen (GNU)
2. dtach
3. tmux (BSD)
4. byobu
5. abduco
6. dvtm
7. mtm

## Miscellaneous commands

```
seq         : generates sequence of numbers

rev         : reverses lines of a file (or stdin)

feh         : view image files

              feh -F -Y -z -D 3.5 *.jpg

              feh 
              -F full screen
              -Y hide pointer
              -z randomize
              -D seconds

              commands: ctrl + delete (fn + ctrl + backspace) = deletes file from disk

                        h = pause/continue
                        p = previous image
                        n = next image

```

### ffmpeg

Here is how to create a slideshow from images (1.jpg,2.jpg..,8.jpg) with FFmpeg on your Linux or Unix box:

    $ ffmpeg -y -r 1/3 -framerate 1 -i %1d.jpg  -c:v libx264 -vf fps=5 -pix_fmt yuv420p out.mp4


## od: octal dump

```console
$ od -f pm.0         # outputs number of a binary file interpreted as floats (e.g. PStomo model file)
0000000     4.720000e+00    4.720000e+00    4.720000e+00    4.720000e+00
*
0006740     5.080000e+00    5.080000e+00    5.080000e+00    5.080000e+00
*
0015700     5.440000e+00    5.440000e+00    5.440000e+00    5.440000e+00
*
0024640     5.800000e+00    5.800000e+00    5.800000e+00    5.800000e+00
*
0033600     6.160000e+00    6.160000e+00    6.160000e+00    6.160000e+00
*
0042540     6.520000e+00    6.520000e+00    6.520000e+00    6.520000e+00
*
0051500     6.880000e+00    6.880000e+00    6.880000e+00    6.880000e+00
*
0060440     7.240000e+00    7.240000e+00    7.240000e+00    7.240000e+00
*
0067400     7.600000e+00    7.600000e+00    7.600000e+00    7.600000e+00
*
0076340     7.960000e+00    7.960000e+00    7.960000e+00    7.960000e+00
*
0105300     8.200000e+00    8.200000e+00    8.200000e+00    8.200000e+00
*
0230500
```

Repeated lines are indicated by an asterisk `*`.

```console
$ od -f -v pm.0    # outputs all lines included repeated ones
0000000     4.720000e+00    4.720000e+00    4.720000e+00    4.720000e+00
0000020     4.720000e+00    4.720000e+00    4.720000e+00    4.720000e+00
0000040     4.720000e+00    4.720000e+00    4.720000e+00    4.720000e+00
0000060     4.720000e+00    4.720000e+00    4.720000e+00    4.720000e+00
0000100     4.720000e+00    4.720000e+00    4.720000e+00    4.720000e+00
...
```

In Linux version -w controls the number of bytes per line in output

```console
$ god -f -v -w4 pm.0
0000000            4.72
0000004            4.72
0000010            4.72
0000014            4.72
0000020            4.72
0000024            4.72
0000030            4.72
```

Option address=none does not print the address:

```console
$ god -f -v -w4 -An pm.0

        5.106375
        5.106778
        5.107523
       5.1090393
       5.1125073
```

## Download videos

Twitter videos can be downloaded [here](http://twittervideodownloader.com)
and [here](https://twsaver.com/twitter.php).

To download YouTube videos you can use the `youtube-dl` program (installed using MacPorts):

    $ youtube-dl command-line tool

10 PRINT

    $ env LC_ALL=C tr -c -d '/\' < /dev/random  (or /dev/urandom)

## Unix options

```
Option	Typical meaning

-a	All, append
-b	Buffer,block size, batch
-c	Command, check
-d	Debug, delete, directory
-D	Define
-e	Execute, edit
-f	File, force
-h	Headers, help
-i	Initialize
-I	Include
-k	Keep, kill
-l	List, long, load
-m	Message
-n	Number, not
-o	Output
-p	Port, protocol
-q	Quiet
-r	Recurse, reverse
-s	Silent, subject
-t	Tag
-u	User
-v	Verbose
-V	Version
-w	Width, warning
-x	Enable debugging, extract
-y	Yes
-z	Enable compression
```
