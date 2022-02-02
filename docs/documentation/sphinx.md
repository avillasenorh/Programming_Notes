# Sphinx

`Sphinx` is a Python package to generate documentation of software projects.
By default it uses `rst` format but now it can also use `Markdown`.
does not extract information from the source code files.

## Installation using `pipx`


    $ pipx install sphinx  # check

Sometimes the applications require additional packages (e.g. to add some functionalities). It is 
possible to install additional packages in an existing `pipx` application using `pipx runpip`.
To install the `myst-parser` package that adds capability to use `Markdown` documents:

    $ pipx runpip sphinx install myst-parser

Another useful package is the **Read the Docs** theme:

    $ pipx runpip sphinx install sphinx_rtd_theme


To use Markdown and Read the Docs theme:

```python
import sphinx_rtd_theme

...

extensions = [
    "myst_parser",
    "sphinx_rtd_theme",
]

...

html_theme = 'sphinx_rtd_theme'

```
