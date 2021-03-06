This is a [Pandoc-compatible](http://pandoc.org/README.html) LaTeX style file for writing the DiGRA conference paper in [markdown](http://commonmark.org/). You need Pandoc and some LaTeX installation in order to make the templates work.

This uses `fontspec` for the Arial font, which means you can't use pdflatex as your TeX compiler. Use something like xelatex instead.

Figure 1 is also missing, because it was not part of the original LaTeX template.

If you want a pure LaTeX template, you should use [this repository](https://github.com/adamsumm/DiGRATex) instead.

# Usage

## YAML-section

You must start your markdown-formatted file with a YAML-section, e.g.

	 ---
	 title: "Article Title"
	 author:
	 - name: First Author
	   affiliation: Institutional Affiliation
	 bibliography: bibliography.bib
	 conference: "1^st^ International Joint Conference of DiGRA and FDG"
	 ---

If you wish to anonymize the output, you can set the YAML-variable `anonymous` to `true`. That will withhold the author name(s) from the start of the document.

## Bibliography

To get the references look right, end the document with

	\theendnotes

	# Bibliography
	
	\newcounter{paras}
	\everypar{%
		\stepcounter{paras}%
		\ifnum\value{paras}>0 
			\hangindent=1cm \hangafter=1
			\setlength{\parskip}{0pt}
	\fi}

These weird commands are necessary to make sure that endnotes are written before the bibliography and the bibliography is formatted properly. See `digra.md` for a complete example file. 

Note that the bibliography uses the complete Chicago format instead of the simpler DiGRA format, because there is no [CSL](http://citationstyles.org/) for the DiGRA format.

## Conversion

Convert the paper from markdown to pdf with

	pandoc --pdf-engine=xelatex --filter pandoc-citeproc --template=digra.latex digra.md -o digra.pdf

or use the included Makefile if you have `make` installed.
