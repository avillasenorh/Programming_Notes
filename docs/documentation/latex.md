#LaTeX

LaTeX is a powerful document creation software. It is particularly useful
for long documents and also for displaying math.

Documentation software such as `Mkdocs` and `Sphinx` accept LaTeX code.

## Basic document structure

```latex
% Preamble
\documentclass[12pt, a4paper]{article}
\usepackage[utf8]{inputenc}                      % not needed in modern LaTeX releases
\usepackage{authblk}
\usepackage{graphicx}
\graphicspath{ {Figures/} }

% Title and author(s)
\title{Skeleton for LaTeX articles}
\author[1]{Antonio Villaseñor}
\author[2,3]{Another Author}
\affil[1]{Institute of Marine Sciences (ICM), CSIC,
 Pg. Maritim de la Barceloneta 37-49, E-08003 Barcelona, Spain}
\affil[2]{Some Institute}
\affil[3]{Some University}

\date{\today} % write today's date (default)

% Body of the document with numbered and un-numbered sections and bibliography
\begin{document}
\maketitle
\newpage

\begin{abstract}
\end{abstract}

\section{Introduction}

\section{Data}

\section{Methods}

\section{Results}

\section{Discussion}

\section{Conclusions}

\section*{Data and Resources}                    % asterisk disables numbering of this section

\section*{Acknowledgments}

\bibliography{references}                        % generate reference list using file references.bib

\end{document}
```

## Preamble

Sets the type of document (article, book, etc), and all the packages that will be used.

The first element is the document class. To create the simplest document use for example:

```
\documentclass{minimal}

\begin{document}

Minimal document.

\end{document}
```

Typical packages:

- `geometry`: set page size and margins
- `inputenc`: allows to use accented characters directly
- `fontenc`: ?
- `amsmath`, `amssymb`, `amsfonts`, `latexsym`: AMS symbols and math
- `mathptmx`: use times as default font, and provide maths support (outdated?)
- `authblk`: handle authors and affiliations
- `babel`: use other languages
- `lineno`: add line numbers
- `graphicx`: handle figures (extended version of `graphic`)

Example of a preamble using the above packages:

```
\documentclass[a4paper, 12pt]{article}
\usepackage{amsmath,amssymb,amsfonts,latexsym}
%\usepackage[utf8]{inputenc}
\usepackage[latin1]{inputenc}
\usepackage[T1]{fontenc}               # better than default encoding OT1 (?)
\usepackage{authblk}

\usepackage{graphicx}
\graphicspath{ {Figures/} }

\usepackage{lineno}
\linenumbers

```

## Citations

The standard LaTeX command `\cite` does not have enough flexibility and should be avoided.
Instead use the non-standard commands `\citep` and `\citet` provided by the `natbib` package.

To use the `natbib` package, the following line must be added in the preamble:

```
\usepackage[round, semicolon, sort&compress, authoryear]{natbib} # round, semicolon, and authoryear are default options
```

To cite using **textual notation** as in: _Allen (1978)_ use:

```
\citet{Allen1978}
```

To cite using **parenthetical notation** as in: _(Allen, 1978)_ use:

```
\citep{Allen1978}
```

To cite between parenthesis with text **after** citation: _(Allen, 1978, p. 100)_ use:

```
\citep[p.~100]{Allen1978}
```

To cite between parenthesis with text **before** citation: _(e.g., Allen, 1978)_ use:

```
\citep[e.g.,][]{Allen1978}
```

To cite between parenthesis with text **before and after** citation: _(see Allen, 1978, chap. 2)_ use:

```
\citep[see][chap.~2]{Allen1978}
```

Commands `\citep*{many_authors}` and `\citet*{many_authors}` lists all the authors instead
of the abbreviated list. E.g., _(Johnson, Lewis, and Watson, 1990)_.


