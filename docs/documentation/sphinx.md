# Sphinx

`Sphinx` is a Python package to generate documentation of software projects.
By default it uses `rst` format but now it can also use `Markdown`.
does not extract information from the source code files.

## Installation using `pipx`


    $ pipx install sphinx  # check

Sometimes the applications installed with `pipx` require additional packages (e.g. to add
some functionalities, such as additional themes, ...). It is 
possible to install additional packages in an existing `pipx` application using `pipx runpip`.
To install the `myst-parser` package that adds capability to use `Markdown` documents:

    $ pipx runpip sphinx install myst-parser

Other useful packages art the **Read the Docs** and **Furo** themes:

    $ pipx runpip sphinx install sphinx_rtd_theme
    $ pipx runpip sphinx install furo


To use Markdown and Read the Docs theme:

```python
import sphinx_rtd_theme

...

extensions = [
    "myst_parser",
    "sphinx_rtd_theme",
]
...

html_theme = "sphinx_rtd_theme"

```

To use the Furo theme simply:

```python
html_theme = "furo"
```

## Changing from reStructuredText to Markdown

Once added the `myst_parser` extension in `conf.py` we can change
`index.rst` for `index.md`.

An initial file `index.rst` looks like:

```
.. test documentation master file, created by
   sphinx-quickstart ...

Welcome to test's documentation!
================================

.. toctree::
   :maxdepth: 2
   :caption: Contents:

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
```

The equivalent Markdown file `index.md` would be:

````
% test documentation master file, created by
% sphinx-quickstart

# Welcome to test's documentation!

```{toctree}
:maxdepth: 2
:caption: "Contents:"
```

# Indices and tables

- {ref}`genindex`
- {ref}`modindex`
- {ref}`search`

````

```



## Inserting figures

Local and remote figures can be inserted using standard Markdown syntax:

```markdown
![remote logo here](https://..../logo.png)

![local logo here](logo.png)
```

Myst-Sphinx also allows more options but first you need to add and extension in `conf.py`:

```python
myst_enable_extensions = [
    "colon_fence",
]
```

You can use rest:

````
```{image} logo.png
:alt: local logo here
:class: bg-primary
:width: 200px
:align: center
```
````

You can also use HTML:

```
:::{figure-md} logo-target
:class: myclass

<img src="logo.png" alt="local logo here" class="bg-primary" width="300px">

Here Python logo
:::
```

## Download

You can download the file `logo.png` for offline use.

    {download}`logo.png`

    {download}`the logo <logo.png>`

Normal markdown link [text](linked_document)

this [](linked_document) gets the text from the linked document title


## Some roles

Define role somewhere in your documents as:

    (investors)=

Then use this to refer to

    {ref}`investors`

This might work to change your linked text:

    {ref}`another text <investors>`


## Code blocks

Normal markdown:
````
```python
print("hola")
```
````

myst

````
```{code-block} python
:linenos:
print("hola")
```
````

Code from file:

This includes the entire file:
  
````
```{literalinclude} my_file.py
```
````

For more options:

````
```{literalinclude} my_file.py
:emphasize-lines: 2-3
```
````




