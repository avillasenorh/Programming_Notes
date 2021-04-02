# Doxygen

[Doxygen](https://www.doxygen.nl/index.html) is a tool to generate documentation from source code.
It can be installed for macOS using a `dmg` file provided in the [downloads page](https://www.doxygen.nl/download.html).

## Doxygen for C projects

If Doxygen has been installed with a `dmg` file, the executable will be located
in the `/Applications` folder. It is then useful to generate an alias for the
executable so it can be run from the command line:

    $ alias doxygen='/Applications/Doxygen.app/Contents/Resources/doxygen'

Go to source directory and generate configuration file:

    $ cd src/project
    $ mkdir docs
    $ doxygen -g project.cfg

Edit `project.cfg` and change the following parameters:

```
35c35
< PROJECT_NAME           = "C date-time"
---
> PROJECT_NAME           = "My Project"
47c47
< PROJECT_BRIEF          = "Utilities to handle dates and times using standard C structures and functions"
---
> PROJECT_BRIEF          =
61c61
< OUTPUT_DIRECTORY       = /Users/antonio/Dropbox/src/tests/C_time/docs
---
> OUTPUT_DIRECTORY       =
208c208
< JAVADOC_BANNER         = YES
---
> JAVADOC_BANNER         = NO
272c272
< OPTIMIZE_OUTPUT_FOR_C  = YES
---
> OPTIMIZE_OUTPUT_FOR_C  = NO
464c464
< EXTRACT_ALL            = YES
---
> EXTRACT_ALL            = NO
```

To search for source code in subdirectories:

    RECURSIVE = YES 

For Python use:

    OPTIMIZE_OUTPUT_JAVA   = YES (instead of OPTIMIZE_OUTPUT_FOR_C)

To generate documentation:

    $ doxygen project.cfg

    $ open docs/html/index.html


Example of documentation of a function:

```C
/**
 ** @brief Print a @c timespec structure into a string using the ISO8601 format
 **
 ** ISO 8061 format is: YYYY-MM-DDTHH:MM:SS.FFFFFFFFF
 **
 ** @param[out]  sdate   string with date-time in ISO 8601 format
 ** @param[in]   ts      timespec structure containing a valid date-time
 */
```

## Doxygen for Python projects

Contrary to the official documentation, "special commands" are supported in docstrings.
To do this the docstring must start with `"""!` (not tested!!!)

Example:

```python
def area(l, w):
    """! Calculate the area in sqm

    @param l length 
    @param w width
    @return area 

    @todo throw error if l<0 or w<0
    """
    return l*w
```

