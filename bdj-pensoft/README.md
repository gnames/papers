# Biodiversity Data Journal (Pensoft) template

## Bibliography style

The style was picked by `Search by example` at [Mendeley]

`refs.csl` file uses [Journal of Tropical Science] style

## Pandoc commands

### Generate Tex

The `-C` or `--citeproc` flag generates citations using `cls` and
`bibliography` directives from a markdown file.

```bash
pandoc -C -s test.md -o test.tex
```

### Generate PDF

```bash
pandoc -C -s test.md -o test.pdf
```

### Generate text from Latex

```bash
detex test.tex > test.txt
# or
pdftotext test.pdf > test.txt
# or even
gnfinder -I test.pdf > test.txt
```

[Mendeley]: https://csl.mendeley.com/searchByExample/
[Journal of Tropical Science]: http://www.zotero.org/styles/journal-of-tropical-life-science

