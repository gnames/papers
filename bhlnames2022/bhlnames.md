---
title: BHLnames
author: John Doe, Jane Doe
date: 2021-10-27
csl: refs.csl
bibliography: bhlnames.bib
geometry: margin=2cm
header-includes:
  - \hypersetup{colorlinks=false,
    allbordercolors={0.6 0.6 1},
    pdfborderstyle={/S/U/W 0.5}}
---

# Abstract

## Background

* BHL exists
* CoL exists
* Global Names exists
* BHL has index
* COL has names with nomenclatural publications

## New information

* BHlnames now exists
* BHLnames solves these 3 problems
* Can access via web
* Can access via API
* Can see name->description via file
* Local use is possible

# Keywords

biodiversity informatics, biodiversity heritage library, catalogue of life,
global names, nomenclature, taxonomy, library informatics

# Classifications

## Taxon Classification

? Animalia, Plantae, all other from the list

## Subject classification

Bioinformatics

# Funder

Species File Group, BHL index

# Introduction

* Biodiversity "layers"
  ~ 100mil name-strings (lexial layer)
  ~ 7mil names (nomenclatural layer)
  ~ 2.5mil taxons
* CoL
  - exists since ?
  - goal all species (global scope)
  - covers taxonomy and, to a degree, nomenclatural layers
  - has ~4mil name-strings, ~2m taxons
  - about ?% of name-strings have references
  - taxon/synonymy info allows to find connection from name to taxon to synonyms

Biodiversity Heritage Library (BHL) is the largest open access collection of biodiversity literature.
BHL was founded in 2006 and is goverened by an internetional consortium.
BHL currently comprises of 270 thousand volumes and 60 million pages of biodiversity texts.
By far the best way to discover biodiversity information in BHL is by searching for scintific names of organisms.
The index of scientific names for BHL is created by Global Names Architecture (GNA) project.

The purpose of GNA is creation of services and tools that allow to globally connect biodiversity information and research via scientific names.
GNA was founded in 2007 and includes nomenclatural (ZooBank, a zoological names registrator) and lexical tools (GNparser, GNverifier, GNfinder).
GNfinder detects scientific names in texts.
GNparser normalizes scientific name-strings and extracts semantic meanings of their components.
Normalised scientific names allow to aggregate lexical variants of a name into a lexical group.
GNverifier allows to search a name-string of interest in more than 100 sources of biodiversity data.
GNverifier uses data from Catalogue of Life, Encyclopedia of Life, Index Fungorum, Global Biodiversity Information Facility and many others.
GNA tools are used for creation of scientific name index in BHL.

The BHL index of scientific names is created by processing BHL data through BHLindex, yet another GNA tool.
BHLindex breaks each volume in BHL into tokens (words).
Then it scans the tokens and uses heuristic and natural language processing algorithms of GNfinder to detect possible scientific names.
Later these names are verified (reconciled and resolved) via GNverifier.
The process is quite fast and allows to process 60 millions of BHL pages in about 12 hours on a modern laptop.
The efficiency of the index creation allows to incrementally improve algorithms and quality of the name-finding.
GNverifier also provides metadata for each volume, calculating its biological "context".
Such information includes the kingdom which contains most of the names found in a volume, as well as the lowest clade that contains more than half of the volume' names.
The calculation uses managerial classification of the Catalogue of Life.

Searching BHL for a particular name in the name index would often miss a significant amount of data because taxons' names do change with time.
CoL currently contains ~4 million names, for ~2 million taxons.
The database of GNverifier contains 8 million canonical forms, for ~2.5 million known taxons.
From this data we can estimate that there are 2-3 names per a taxon on average.
It means that to get more comprehensive data about species it is important to search not only by one name, but by all names used for the species historically.

Another way to aquire information from BHL is by searching for a particular paper.
Thanks to BioStore effort metainformation and location is known for 200 000? papers in BHL. However to find a paper by a citation is still hard, especially automatically by a script.
There is a large variety of lexical variants for every journal name (FIG).
Format of data about the year of publication, a journal volume, pages differs from one citation to the next.
It is much easier to search for a year, volume and page data as numbers, but in BHL such metadata is stored as a string and is not consistent throghout the corpus.
Quite often such metadata is missing, or contains mistakes and it makes the search harder.

TODO: Fig: examples of journal name different spellings

If a researcher has a citation of a nomenclatural event and tries to find the paper with original description of species, it is often not a trivial task.
Citations are hard to match to pages in BHL as described above.
Sometimes OCR errors change a name spelling and as a result exist in a volume under different spelling variants.
Quite often people add an annotation next to new species or combination, such as sp.nov, comb nov.

However such annotations are not consistent (FIG), and also often modified by OCR.
When several species of the same genus are described, the genus in the name is often abbreviated, which also masks the name from a researcher.

TODO: Fig: examples for annotations

The project we describe in this paper helps to adress these problems with the following solutions.
BHLnames uses name index, CoL data, and BHL metadata together to improve search of an information connected to a name-string, match a citation to a page in BHL, find pages that contain original descriptions of species..
BHLnames uses CoL synonymy data to optionally expand name search to all its synonyms.
BHLnames normalizes BHL data for publication years and pages, making it easier to compare it with numeric representations of years and pages.
The project uses 2? million citations of nomenclatural events for names in CoL to provide data about nomenclatural events.
BHLnames normalizes journal names in a citation and BHL to match them together.
We use Naive Bayes approach to calculate probabilities of a citation to a BHL page match and return the best results.
Such results are provided via Dryad (Link)

# Project description


Title: BHLnames

Study area description: Biodiversity Informatics

Design description: This is the whole paper actually (?)

## Goals

The goals of BHLnames project are:

1. Provide an ability to search for a citation in BHL using citation metadata
and the index of names data.

    Use names' index information to dramatically simplify search for a publication.
    Combine citation metadata together with occurences of a name to point to possible pages of a citation with high probability.

2. Discover original descriptions and nomenclatural events in BHL.

    Use the goal #1 together with citation and name information from CoL.
    Combine these data to determine pages containing nomenclatural events for scientific names.
    Increase usability of BHL for biodiversity reseearchers by augmenting scientific names index with the nomenclatural events index.

3. Add "taxonomic intalligence" to the BHL's index of scientific names.

    Use goal #2 and the CoL data to optionally expand BHL name search with taxonomical information.
    Return data not only for a particular name, but for its synonyms.
    Provide data about currently accepted name for the taxa.
    Also, when available, provide data about nomenclatural events for all relevant names.

(Methods)

## Architecuture

### Dependencies

### Project structure

### Workflow

#### Data Import

## Interfaces

### GUI

### Embeddable widget

### API

### Command line

### Input formats

## Audience

CoL
ZooBank
WoRMS?
TW
BHL users
  Taxonomists
  Librarians
  Citizen Scientists
  Nomenclators
  Other Reseachers

(Results)

### Examples of usages

### Summary of scores

### Benchmarks

### Open data deliverables

(Discussion)

## Conclusions

- Jigsaw puzzle where a name is the first piece.
- We add more pieces

Advantages, impact

Missing parts

Ways to improve

How it helps for the other future developments

How to contribute?

Funding: skip it here? Same as above

# Web location (URIs)

Homepage: bhlnames.globalnames.org

Wiki: github.com/gnames/bhlnames wiki (maybe, or nothing)

Download page: data or code?
  * code: https://github.com/gnames/bhlnames
  * data: some place on Dryad?

Download mirror: n/a

Bug database: https://github.com/gnames/bhlnames/issues

Mailing list: https://gitter.io/gnames/something ?

Blog: http://globalnames.org

Vendor: N/A ask Matt

# Technical specification

Platform: ?

Programming language: Go, JavaScript?

Operating system: GNU/Linux

Interface language: JavaScript?

Service endpoint:
  * https://bionames.globalnames.org/api/v1
  * https://apidoc.globalnames.org/bhlnames

# Repository

Type: Git

Browse URI: https://github.com/gnames/bhlnames

Location: ?

Module: ?

Anonymous root: n/a

# Usage license

MIT

# Implementation

Implements specification: N/A

Audience:

# Additional information

# Acknowledgements

Thanks to you all. Rich Pyle for journal data

# Author contributions

# References

# Figures

# Tables

# Supplementary material

# Endnotes


