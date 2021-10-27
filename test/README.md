# test playground for generating papers via markdown and pandoc

## Bibliography style

`refs.csl` file uses [Journal of Tropical Science] style

## Pandoc commands

### Generate Tex

```bash
pandoc -C -s test.md -o test.tex
```

### Generate PDF

```bash
pandoc -C -s test.md -o test.pdf
```


[Journal of Tropical Science]: http://www.zotero.org/styles/journal-of-tropical-life-science

