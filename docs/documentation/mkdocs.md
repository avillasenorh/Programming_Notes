# MkDocs

`MkDocs` is a Python package to generate documentation of software projects. It uses `Markdown`
documents to generate the web pages. It is ideal for documenting the use of sofware packages,
tutorials, and notes like these. Unlike other documentation packages (to my understanding), it
does not extract information from the source code files.

## Installation using `pipx`

The task of creating and activating an environment to install a Python app can be simplified using
`pipx`. This tool installs and runs Python applications from isolated environments. Once installed,
these applications can be run from the command line without the need to activate the environment.
The virtual environments are usually in `~/.local/pipx/venvs` and the applications are soft links
in `~/.local/bin`. This last directory must be included in the `$PATH` environmental variable.

The applications are installed using the command `pipx install`:

    $ pipx install mkdocs

Sometimes the applications require additional packages (e.g. to add some functionalities). It is 
possible to install additional packages in an existing `pipx` application virtural environment using `pipx runpip`.
To install the `python-markdown-math` package that adds math expressions using LaTeX:

    $ pipx runpip mkdocs install python-markdown-math

To install the [Material](https://squidfunk.github.io/mkdocs-material/) theme:

    $ pipx runpip mkdocs install mkdocs-material

## Installation using `conda`

    $ conda create -n mkdocs python=3.8
    $ source activate mkdocs
    $ pip install mkdocs
    $ pip install python-markdown-math
    $ pip install mkdocs-material

    $ mkdocs --version
    mkdocs, version 1.1.2 from /Users/antonio/opt/anaconda3/envs/mkdocs/lib/python3.8/site-packages/mkdocs (Python 3.8)


## Getting started

To create a directory for documentation files:

    $ mkdocs new mkdocs_test
    INFO    -  Creating project directory: mkdocs_test
    INFO    -  Writing config file: mkdocs_test/mkdocs.yml
    INFO    -  Writing initial docs: mkdocs_test/docs/index.md

creates a directory called `mkdocs_test` with the following files:

    mkdocs.yml
    docs/
    docs/index.md

To create documetation files in an existing directory:

    $ cd my_project
    $ mkdocs new .
    INFO    -  Writing config file: ./mkdocs.yml
    INFO    -  Writing initial docs: ./docs/index.md


Originally the `mkdocs.yml` file contains only the following line:

    site_name: My Docs

Initially the `docs/index.md` file contains the following:
```
# Welcome to MkDocs

For full documentation visit [mkdocs.org](https://www.mkdocs.org).

## Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs -h` - Print help message and exit.

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.
```

## To create web page and server

    $ mkdocs serve &
    $ open http://127.0.0.1:8000/

This allows to preview web page as you work on it (the web page is automatically refreshed)

When done, to generate the web site:

    $ mkdocs build  

This creates a directory named `site` that contains many other directories and
files such as `index.html`, `css/`, ...

    $ mkdocs build --clean  # removes unused files

If you don't want to keep it in **git**, edit `.gitignore` and add:

    site/

Documentation web page can be deployed to GitHub pages. You have to go to
the top directory of the repository (where `mkdocs.yml` is located) and type:

    $ mkdocs gh-deploy

## Editing basic files and adding pages

- Change site_name in mkdocs.yml:
site_name: My Docs


- Add pages

$ curl 'https://jaspervdj.be/lorem-markdownum/markdown.txt' > docs/about.md

This adds an "About" pull down menu from main page.


- Specify pull down menus and menu names in mkdocs.yml (add nav: - do not used tabs for indentation!)
  MkDocs creates menu items from file names in docs/ directory, but it is better to specify it explicitly
  in mkdocs.yml

```
site_name: C++ test programs and libraries

nav:
    - Home: index.md
    - About: about.md
    - Tutorials: tutorials.md
    - Parameters: parameters.md
#theme: readthedocs
```

Each section can have subsections.
Names (section and Markdown files) can be between single quotes.

## Deploy documentation to GitHub

In GitHub create a repository PStomo_documentation and initialize it with a README

Clone repository into local machine:

    $ git clone https://github.com/avillasenorh/PStomo_documentation.git

Copy mkdocs.yml and docs/ to local repository

    $ cp -r mkdocs.yml docs ..../PStomo_documentation/.

Generate site

    $ cd PStomo_documentation
    $ mkdocs build [--clean]

    $ git add -A
    $ git commit -m "Initial build"
    $ git push

    $ mkdocs gh-deploy

Creates web site: [https://avillasenorh.github.io/PStomo_documentation/](https://avillasenorh.github.io/PStomo_documentation/)


## Add math equations to MkDocs

To add the capability of displaying mathematical equations, the `python-markdown-math`
package is required.

The file `mkdocs.yml` must be edited so it can use the Markdownn extensions from this
package. This is done adding the following lines:

```
site_name: My Docs

extra_javascript:
    - https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.4/MathJax.js?config=TeX-AMS-MML_HTMLorMML

markdown_extensions:
    - mdx_math
```
WARNING: version of `mathjax` changes, so using an older version might be incompatible
with newer versions of MkDocs.

Test web page editing docs/index.md:

```
# MathJax Test Page

When \(a \ne 0\), there are two solutions to \(ax^2 + bx + c = 0\) and they are
$$x = {-b \pm \sqrt{b^2-4ac} \over 2a}.$$
```
Produces the following output:

When \(a \ne 0\), there are two solutions to \(ax^2 + bx + c = 0\) and they are
$$x = {-b \pm \sqrt{b^2-4ac} \over 2a}.$$

## Resources

- [The best MkDocs plugins and customizations](https://chrieke.medium.com/the-best-mkdocs-plugins-and-customizations-fc820eb19759)
- [Mermaid](https://mermaid-js.github.io/mermaid/#/) diagrams using text and code
  ([GitHub](https://github.com/mermaid-js/mermaid))
- [Material](https://squidfunk.github.io/mkdocs-material/) for MkDocs
- [MkDocs is the Perfect Open Source Documentation Software](https://fosspost.org/mkdocs-perfect-open-source-documentation-software/)
- MkDocs [Wiki](https://github.com/mkdocs/mkdocs/wiki)
- MkDocs [GitBook theme](https://gitlab.com/lramage/mkdocs-gitbook-theme)
- MkDocs [plugins](https://github.com/mkdocs/mkdocs/wiki/MkDocs-Plugins)
- [mkdocstrings](https://github.com/mkdocstrings/mkdocstrings)

