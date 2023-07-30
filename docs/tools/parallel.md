# Parallel

Simple run: a command that reads an argument:

```
$ parallel echo ::: A B C
B
C
A
```

This is equivalent to:

```
$ parallel echo {} ::: A B C
$ parallel echo {1} ::: A B C
```

`parallel` can also read 2 arguments:



