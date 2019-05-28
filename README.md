UnB/MAT Modelo de Dissertações e Tese
=====================================



[![Join the chat at https://gitter.im/kks32/phd-thesis-template](https://badges.gitter.im/kks32/phd-thesis-template.svg)](https://gitter.im/kks32/phd-thesis-template?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
> Modelo de Teses e dissertações - Departamento de Matemática - Universidade de Brasília.

[![License MIT](http://img.shields.io/badge/license-MIT-brightgreen.svg)](license.md)
[![Version](http://img.shields.io/badge/version-0.1-brightgreen.svg)](https://github.com/deividrvale/unb-thesis-template)

## Autor
* Daniele Nantes
* Deivid Vale

--------------------------------------------------------------------------------
## Features

* Modelo Baseado no trabalho de Krishna Kumar [https://github.com/kks32/phd-thesis-template](https://github.com/kks32/phd-thesis-template). Modificado para se adequar aos padrões da Universidade de Brasília.

* Suporta LaTeX, XeLaTeX and LuaLaTeX.

* Título Adaptável: Texto se adapta de acordo com o tamanho do título.

* Logotipo da Universidade de Brasília de acordo com as regras da Marca UnB.

* Versões para imprenssão e online.

* Suporta mudança de estilo de Bibliografia (authoryear / numbered / custom).

* Margens pré-definidas e customizáveis.

* Modo rascunho.

--------------------------------------------------------------------------------

## Compilando sua Tese - XeLaTeX

### usando latexmk (Unix/Linux/Windows)

O modelo suporta `XeLaTeX` . Para gerar o PDF manualmente execute

    latexmk -xelatex thesis.tex
    makeindex thesis.nlo -s nomencl.ist -o thesis.nls
    latexmk -xelatex -g thesis.tex

### usando latexmk (Unix/Linux/Windows)

O modelo suporta `LuaLaTeX` para gerar o PDF execute

    latexmk -pdflatex=lualatex -pdf thesis.tex


## compilando com - LaTeX / PDFLaTeX

### usando latexmk (Unix/Linux/Windows)

O modelo suporta `latexmk`. Para gerar o PDF execute

    latexmk -dvi -ps -pdf thesis.tex

### Shell script para PDFLaTeX (Unix/Linux)

Uso: `sh ./compile-thesis.sh [OPTIONS] [filename]`

[option]  compile: Compila a tese e atualiza todos os índices, figuras e referências.

[option]  clean: remove arquivos temporários.

### Usando o arquivo bat no Windows (PDFLaTeX)

* Abra o prompt de comando, navegue até a pasta do projeto. Execute:

    `compile-thesis-windows.bat`.

* Ou então, execute normalmente `compile-thesis-windows.bat`


-------------------------------------------------------------------------------

## Configurações Iniciais

Informações da dissertação como título, autor, ano, grau, etc., além de outras meta-informações podem ser modificadas em `thesis-info.tex`

### Class options

The class file, `PhDThesisPSnPDF`, is based on the standard `book` class

It supports the following custom options in the documentclass in thesis.tex:

(Usage `\documentclass[a4paper,11pt,print]{Classes/PhDThesisPSnPDF}`)

*   `a4paper` (default as per the University guidelines) or `a5paper`: Paper size

*   `11pt` or `12pt`: The University of Cambridge guidelines recommend using a minimum font size of 11pt (12pt is preferred) and 10pt for footnotes. This template also supports `10pt`.

*   `oneside` or `twoside` (default): This is especially useful for printing double side (twoside) or single side.

*   `print`: Supports Print and Online Version with different page margins and hyperlink styles.
    Use `print` in the options to activate Print Version with appropriate margins and page layout and view styles.
    Leaving the options field blank will activate Online version.

*   `custommargin`: You can alter the margin dimension for both print and online version by using the keyword `custommargin` in the options. Then you can define the dimensions of the margin in the `preamble.tex` file:

        \ifsetCustomMargin
          \RequirePackage[left=37mm,right=30mm,top=35mm,bottom=30mm]{geometry}
          \setFancyHdr
        \fi
    `\setFancyHdr` should be called when using custom margins for proper header/footer dimensions

    `\ifsetMargin` is deprecated, please use `\ifsetCustomMargin` instead.

*   `index`: Including this option builds the index, which is placed at the end of the thesis.

    Instructions on how to use the index can be found [here](http://en.wikibooks.org/wiki/LaTeX/Indexing#Using_makeidx).

    _Note_: the package `makeidx` is used to create the index.

*   `abstract`: This option enables only the thesis title page and the abstract with title and author to be printed.

*   `chapter`: This option enables only the specified chapter and it's references. Useful for review and corrections.

*   `draft`: The default draft mode supports some special features such as line numbers, images, and water mark with
    timestamp and custom text. Position of the text can be modified in `preamble.tex`.

*   `draftclassic`: This mode is similar to the default draft mode in the book class. Images are not loaded.

*   `lineno`: Enables pagewise line numbering on the outer edge. You can switch-off line numbering by specifying `nolineno` in the options.

*   `flushleft`: The University recommends using ragged right or flush left alignment for texts. The reason behind this is left justifying a text may exclude a certain readers. Dyslexic people find it hard to read justified text. You can enable `raggedright` option in the document class by passing `flushleft` argument. Default is flush left and right.

### Title page

The front page (title page) resizes to fit your title length. You can modify the options in `thesis-info.tex`.

* `\subtitle` (optional): Adds a subtitle to your thesis.

* `\college` (optional): This option adds the name of your college on the bottom left.

If `\college` is defined, the bottom of the title page will look like this:

        King's College 			                                         2014

If `\college` is undefined or blank, the `degreedate` will be centered.

                                        2014

The template offers support to having both the college and university crests or just one of the crests.

* `\collegeshield` (optional): Includes college crest in addition to the university crest. This reformats the front page layout.

### Abstract separate

*  A separate abstract with the title of the PhD and the candidate name has to be submitted to the Student Registry. This can be generated using `abstract` option in the document class. Ignore subsequent warnings about skipping sections (if any).

*  To generate the separate abstract and the title page, make sure the following commands are in the preamble section of `thesis.tex` file:

        \ifdefineAbstract
        \includeonly{Abstract/abstract}
        \fi

### Chapter mode

*  The chapter mode allows user to only print specific chapters along with references. By default, it excludes everything else in the front matter and appendices. This can done by using `chapter` option in the document class in `thesis.tex`. Ignore subsequent warnings about skipping sections (if any).

*  To generate the separate abstract and the title page, make sure the following commands are in the preamble section of `thesis.tex` file:

		\ifdefineChapter
			\includeonly{Chapter3/chapter3}
		\fi

### Draft

`draft` adds a watermark `draft` text with timestamp and version number at the top or
the bottom of the page. Pagewise line numbering is added on every page. `draft` settings can be tweaked in the `preamble.tex`.

* Use `draftclassic` in the document class options to use the default book class draft mode.

* To add figures in draft mode (default enabled), in the preamble set `\setkeys{Gin}{draft=false}`. `draft=true` disables figures

* To change the watermark text
      \SetDraftText{DRAFT}

* To change the position of the watermark text. Default watermark position is top. The location can be changed to (top / bottom)
      \SetDraftWMPosition{bottom}

* To change the draft version. Default draft version is v1.0.
      \SetDraftVersion{v1.1}

* Watermark grayscale value can be modified. Text grayscale value (should be between 0-black and 1-white). Default value is 0.75
      \SetDraftGrayScale{0.8}


### Choosing the fonts

`PhDThesisPSnPDF` currently supports three fonts `Times`, `Fourier` and `Latin Modern (default)`.

*   `times`: (The University of Cambridge guidelines recommend using Times). Specifying times option in the document class will use `mathptpx` or `Times` font with Math Support.
*   `fourier`: fourier font with math support
*   `default (empty)`: When no font is specified, `Latin Modern` is used as the default font with Math Support.
*   `customfont`: Any custom font can be set in preamble by using `customfont` option in the document class. Then the custom font can be loaded in preamble.tex in the line:

		\ifsetCustomFont
		  \RequirePackage{Your_Custom_Font}
		\fi

### Choosing the bibliography style

`PhDThesisPSnPDF` currently supports two styles `authoryear` and `numbered (default)`. Citation style has to be set. You can also specify `custombib` style and customise the bibliography.

* `authoryear`: For author-year citation eg., Krishna (2013)

* `numbered`: (Default Option) For numbered and sorted citation e.g., [1,5,2]

* `custombib`: Define your own bibliography style in the `preamble.tex` file.

		\RequirePackage[square, sort, numbers, authoryear]{natbib}

* (Overview of Bibtex-Styles with preview)[http://nodonn.tipido.net/bibstyle.php?]

* If you would like to use biblatex instead of natbib. Pass the option `custombib` in the documentclass. In the `preamble.tex` file, edit the custombib section. Make sure you don't load the natbib package and you can specify the layout of your references in `thesis.tex` in the reference section. If you are using `biber` as backend, run `pdflatex thesis.tex >> biber thesis >> pdflatex thesis.tex >> biber thesis >> pdflatex thesis.tex`. If you are using the default natbib package, don't worry about this.

### Custom settings

*   The depth for the table of contents can be set using:

		\setcounter{secnumdepth}{3}
		\setcounter{tocdepth}{3}
    A depth of [3] indicates to a level of `\subsubsection` or #.#.#.#. Default set as 2.

*   To hide sections from appearing in TOC use: `\tochide\section{Section name}` in your TeX files

*   Define custom caption style for figure and table caption in `preamble.tex` using:

        \RequirePackage[small,bf,figurename=Fig.,labelsep=space,tableposition=top]{caption}

*   Uncomment the following lines in `preamble.tex` to force a figure to be displayed in a particular location. Use `H` when including graphics. Note `H` instead of `h`.

		\usepackage{float}
		\restylefloat{figure}

*   Bibliography with Author-Year Citation in `preamble.tex`:

        \RequirePackage[round, sort, numbers, authoryear]{natbib}

*   Line spacing for the entire document can be specified in `preamble.tex`. Uncomment the line spacing you prefer. e.g.,
		\onehalfspacing

### Nomenclature definition

* To use nomenclature in your chapters:

        \nomenclature[g-pi]{$\pi$}{ $\simeq 3.14\ldots$}

    The sort keys have prefix. In this case a prefix of `g` is used to denote Greek Symbols, followed by `-pi` or `-sort_key`. Use a `-` to separate sort key from the prefixes. The standard prefixes defined in this class are:

    * `A` or `a`: Roman Symbols

    * `G` or `g`: Greek Symbols

    * `Z` or `z`: Acronyms/Abbreviations

    * `R` or `r`: Superscripts

    * `S` or `s`: Subscripts

    * `X` or `x`: Other Symbols

* You can change the Title of Nomenclature to Notations or Symbols in the `preamble.tex` using:

        \renewcommand\nomname{Symbols}

 TexStudio's default compile option doesn't include `nomenclature`, to compile your document with the nomenclature, do the following:

    Options >> Configure TexStudio >> Build >> User Commands >> add user command
In `add user command` type `makenomeclature:makenomenclature` on the left pane and `makeindex %.nlo -s nomencl.ist -o %.nls` on the execution side. Now you can run the user defined command `makenomenclature` from `Tools >> User >> makenomenclature`.

Alternatively, you can use the `compile-thesis-windows.bat` file or run `make` on Unix / Linux / MacOS

## General guidelines
[Why is it important to follow good practices and not get killed by a Velociraptor ;)](http://www.xkcd.com/292/)

* To restrict the length of the figure caption in List of figures use a \[short-title\] and {longtitle} for the caption or the section:

    `\caption[Caption that you want to appear in TOC]{Actual caption of the figure}`
    `\section[short]{title}`

* To exclude sections from being numbered and disable it from appearing in the Table of Contents use \section*{Section_Name} or \chapter*{Chapter_Name}

* To only exclude it from being listed in the Table of Contents encapsulate the section command inside the `\tochide` command. `\tochide{\section{Section_Name}}` the section will not appear in the Table of Contents, but the section will be numbered.

* When including figures in your tex file, it's a good practice to size your picture depending on the page size, instead of using absolute values. In the following example `0.75\textwidth` refers to picture width being set to 75% of the text width.

        \includegraphics[width=0.75\textwidth]{minion}

* Use a `-` to separate sort key from the prefixes, eg., `g-pi` denotes the Greek symbol `pi`.

--------------------------------------------------------------------------------
## Troubleshooting warnings

#### _W1_: I get the LaTeX Warning: You have requested document class `Classes/PhDThesisPSnPDF`, but the document class provides `PhDThesisPSnPDF`, should I be concerned?

No! Do nothing, or if you don't want any warning messages change the line near the top of the class file to \ProvidesClass{Classes/PhDthesisPSnPDF} if you're not going to install the class file in a more standard location. You can install it in a standard location like `/usr/share/texmf/tex/latex/` and run `texhash` to reconfigure.

#### _W2_:I get the package Fancyhdr Warning: \fancyhead's `E` option without twoside option is useless on input line \# or \#. What should I do?

Nothing. The warning is because the twoside option is also defined in the class, although only the oneside option is currently used.

#### _W3_: I get the Class PhDThesisPSnPDF Warning: Unknown or non-standard option 'something'. Will see if I can load it from the book class. If you get a warning unused global option(s): `something` then the option is not supported! on input line \#.

You are either trying to use a undefined option or a non-standard option which is in the book class but not defined in the PhD Thesis Template. If it can be used it will be loaded and you will get no further warnings. If not, the option you chose is unavailable.


#### _W4_: I get LaTeX Warning: Unused global option(s):[something].

You are trying to load an option that is not supported in the PhDThesisClass and the Book Class. Are you sure you are using the right option? Check your spelling!

#### _W5_: I get I'm skipping whatever remains of this command line \# of file thesis.aux \@input{Chapter1/chapter1.aux}

If you are generating a separate abstract for your thesis submission, ignore this warning and good luck with your submission. If you are compiling your thesis and see this warning, please remove the option `abstract` from the document class.

#### _W6_: I get blank pages between chapters

This is normal for a book class. Usually, a new chapter in a book always starts on the right hand side, which is why you see a blank page. You can remove the extra blank page by passing `openany` option to the documentclass. This works for double sided printing. However, if you are printing on a single side, please pass `oneside` option to the document class.

#### _W7_: My references aren't listed in the ordered in which I cite them

This is controlled by the bibliography style. Please use `\bibliographystyle{unsrt}` in `thesis.tex` instead of `apalike`. This applicable only for numerically sorted references.

--------------------------------------------------------------------------------

## Known issue(s) / Bugs / Feature requests

*   Hyperlinks doesn't seem to be working in Post-Script file, however works on DVI and PDF (which is produced from the PS file), possibly viewer limitation than a code bug.

*   On older versions of dvips (version 5.97 or below), if your page margins do not appear properly in your PDF, when compiling through DVI >> PS >> PDF, please ensure that you have set a4paper or a5paper in the document class. If you are still having issues you can run:

		ps2pdf -sPAPERSIZE=a4 thesis.ps thesis.pdf

    This issue occurs only when the papersize is not specified in the document class and you are compiling DVI >> PS >> PDF using an older version (5.97 or below) of dvips.

*   Open issues can be tracked at [https://github.com/kks32/phd-thesis-template/issues](https://github.com/kks32/phd-thesis-template/issues). If you would like a new feature to be added to the template, please create an issue and label it as an enhancement.
*   Please [fork me on github](https://github.com/kks32/phd-thesis-template/fork) and create a pull request, if you would like to contribute to the repo.

--------------------------------------------------------------------------------

## Inspiração/Baseado em

* Modelo Baseado no trabalho de Krishna Kumar [https://github.com/kks32/phd-thesis-template](https://github.com/kks32/phd-thesis-template). Modificado para se adequar aos padrões da Universidade de Brasília.
