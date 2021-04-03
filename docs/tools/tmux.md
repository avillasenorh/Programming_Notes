# tmux

    $ tmux attach   # recover work!

If I exit tmux cleanly (e.g. ^D)

    $ tmux attach
    no sessions


Change prefix from ^B to something else

## Panes

`^B + "`

`^B + %`

`^B + x` (exit) but ^D is faster

`^B + arrow` to change from pane to pane

`^B + z` : zooms on one pane (z again uzooms)

resize panes

`^B` (do not release ^) and use arrows to resized

## Windows

`^B + c` : create a new window

`^B + n,p` : next, previous window 

`^B + &` : kill window

`^B + ,` : rename window

## Sessions

Disconnect for a session:

`^B + d`

    $ tmux attach # connect to a session

or

    $ tmux a

    $ tmux list-sessions

or

    $ tmux ls


    $ tmux attach -t 1 # connect to a session when we have more than one (do not call inside tmux! exit first!
                       # nested sessions are dangerous
or

    $tmux a -t 1

`^B + $` : rename session

Create and name a session:

    $ tmux new -s "session_name" (don't make too long or it truncates name)

Toggle between sessions


`^B + s` (move arrow keys to select session and press ENTER)


## tmux configuration

