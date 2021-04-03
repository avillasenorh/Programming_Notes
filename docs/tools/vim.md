# Vim

Use vim to edit files over the network using ssh on a Linux/Unix/OSX/BSD:

    $ vim scp://user@server//home/user/file

Vim as IDE

    $ cp /usr/share/vim/vim73/vimrc_example.vim ~/.vimrc

The important commands in `.vimrc` for syntax are:

    set nocompatible
    syntax on

In order to recognize `.f` and `.f90`

    $ vi /usr/share/vim/vim73/ftplugin/fortran.vim (insert these commands):

```
let s:extfname = expand("%:e")
if s:extfname ==? "f90"
	let fortran_free_source=1
	unlet! fortran_fixed_source
else
	let fortran_fixed_source=1
	unlet! fortran_free_source
endif
```

    $ vi ~/.vimrc

move the block of text with “syntax on”:
after the block of text with the instruction “filetype plugin indent on”


```console
" Switch syntax highlighting on, when the terminal has colors
" Also switch on highlighting the last used search pattern.
if &t_Co > 2 || has("gui_running")
  syntax on
  set hlsearch
endif

set shiftwidth=4
set tabstop=4
```

Other vim tips:


`:r !pwd` (or another command, such as "date" or "ls -1"


Make a list of numbers in vim:

```
:put=range(1,5)
:put=range(1,10,2)
```

See vim help:

```
:help :put
:help range()
```
