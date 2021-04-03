# Dotfiles

## Login shell

1. run `/etc/profile` (not run in an interactive shell)


```
$ cat /etc/profile
# System-wide .profile for sh(1)

if [ -x /usr/libexec/path_helper ]; then
	eval `/usr/libexec/path_helper -s`
fi

if [ "${BASH-no}" != "no" ]; then
	[ -r /etc/bashrc ] && . /etc/bashrc
fi
```


Last command runs `/etc/bashrc`


```
$ cat /etc/bashrc
# System-wide .bashrc file for interactive bash(1) shells.
if [ -z "$PS1" ]; then
   return
fi

PS1='\h:\W \u\$ '
# Make bash check its window size after a process completes
shopt -s checkwinsize

[ -r "/etc/bashrc_$TERM_PROGRAM" ] && . "/etc/bashrc_$TERM_PROGRAM"
```

Setups `PS1` prompt and checks window size (only for `$TERM_PROGRAM == Apple_Termimal`)

2. Then one of:

```
~/.bash_profile			# this one is read only by bash
~/.bash_login
~/.profile			# this one is read by all shells, not only bash
```

These are local login items.

3. And finally (depending on system???)

`~/.bashrc`

To keep the environment consistent between non-login and login shells, source the `.bashrc` from `.bash_profile`

```
if [ -f ~/.bashrc ]; then
        . ~/.bashrc
fi
```

## Not a login shell

[0. run /etc/bash.bashrc ?]

1. run .bashrc

There is a template for .bashrc in /etc/bashrc

```
$ cat /etc/bashrc
# System-wide .bashrc file for interactive bash(1) shells.
if [ -z "$PS1" ]; then
   return
fi

PS1='\h:\W \u\$ '
# Make bash check its window size after a process completes
shopt -s checkwinsize

[ -r "/etc/bashrc_$TERM_PROGRAM" ] && . "/etc/bashrc_$TERM_PROGRAM"
```


## macOS

Apparentely the OSX Apple Terminal and iTerm2 always open a login shell.
Character (login or non-login) can be determined by leading "-" in $0 (need to make sure):

% echo $0
-/bin/tcsh
$ bash
$ echo $0
bash


## Non-interactive shell

Executes the commands in the startup file indicated by variable BASH_ENV
The default value of this variable is usually undefined

This means that in a bash shell script no configuration file is executed???
Then variables are inherited from the shell that calls it??

Common cases (options --login, --noprofile, --rcfile, --norc, not used)

Interactive, Login:      /etc/profile, (~/.bash_profile | ~/.bash_login | ~/.profile), [~/.bashrc]
Interactive, Non-Login:  /etc/bash.bashrc, ~/.bashrc
Non-Interactive:         $BASH_ENV   (This means all variables inherited from parent shell?
                                      What if shell is called from at, cron, etc?)

In OS X all terminal applications open a login shell.
Therefore all parameters must be in ~/.bash_profile or make that ~/.bash_profile sources ~/.bashrc

In OS X /etc/bash.bashrc does not exist


## Shell options

    $ shopt (lists shell options)

an important one is "huponexit" (background jobs continue to run when closing shell)




