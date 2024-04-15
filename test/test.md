---
title: Paper generation via Pandoc
author: John Doe, Jane Doe
date: 2021-10-27
geometry: "left=2cm,right=2cm,top=2cm,bottom=2cm"
bibliography: refs.bib
csl: refs.csl
mainfont: DejaVuSerif.ttf
mainfontoptions:
- BoldFont=DejaVuSerif-Bold.ttf
- ItalicFont=DejaVuSerif-Italic.ttf
- BoldItalicFont=DejaVuSerif-BoldItalic.ttf
sansfont: DejaVuSans.ttf
monofont: DejaVuSansMono.ttf
output: pdf_document
---

# Abstract

Lorem ipsum

# 1. Background

\begin{tabular}{|l|l|}\hline
Age & Frequency \\ \hline
18--25  & 15 \\
26--35  & 33 \\
36--45  & 22 \\ \hline
\end{tabular}

\begin{}
\nocite{ICPN}
\nocite{FNA2002}
\end{}

::: {#refs}
:::

# Acknowledgements

Thanks to you all

# Bibliography
