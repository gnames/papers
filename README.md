# Global Names papers

Collection of papers prepared to describe Global Names projects

## Alias for setting windows and running auto PDF generation

```bash
alias pps="cd ~/papers && vi -c NotesLayout"
```

## Using [guard] for automatic PDF compiling

1. Install full `latex` package for your OS
2. Install `pandoc` and its dependencies
3. Go to `papers` directory (see the alias above).
4. Run `bundle` command from the root to install required gems
5. Set a script `$HOME/bin/pdcit` in your execution path

An example of `pdcit`:

```bash
#!/bin/bash

path=$(dirname ${1})
file=$(basename ${1} ".md")
cd ${path}
pandoc -C -s "${file}.md" --pdf-engine=xelatex --highlight-style \
  zenburn -o "${file}.pdf"
pandoc -C -s "${file}.md" -o "${file}.tex"
cd -
```

## Directory

test
: a playground for pandoc-based PDF/Latex generation

[guard]: https://github.com/guard/guard
