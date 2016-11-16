Master's Project
================

This is the repository for my M.Sc. Dissertation.

## Compile the report

Thanks to awesome [pandoc](http://programminghistorian.org/lessons/sustainable-authorship-in-plain-text-using-pandoc-and-markdown), I can write the report mostly in markdown, math
symbols are required to be in `$` or `$$`. I use [zotero](http://zotero.org/) to manage and compile
the bibliography. To convert the report to pdf use the following command:

```
pandoc report.md --filter=pandoc-citeproc -o report.pdf --latex-engine=xelatex --template=template.tex
```
