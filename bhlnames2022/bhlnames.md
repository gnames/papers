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

Biodiversity Heritage Library (BHL) is the largest open access collection of
biodiversity literature.
BHL was founded in 2006 and is goverened by an internetional consortium.
BHL currently comprises of 270 thousand volumes and 60 million pages of biodiversity texts.
By far the best way to discover biodiversity information in BHL is by searching for scintific names of organisms.
The index of scientific names for BHL is created by Global Names Architecture (GNA) project.

The purpose of GNA is creation of services and tools that allow to globally connect biodiversity information and research via scientific names.
GNA was founded in 2007 and includes nomenclatural (ZooBank, a zoological names registrator) and lexical tools (GNparser, GNverifier, GNfinder).
GNfinder detects scientific names in texts.
GNparser normalizes scientific name-strings and extracts semantic meanings of
their components.
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
Such information includes the kingdom which contains most of the names found
in a volume, as well as the lowest clade that contains more than half of
the volume' names.
The calculation uses managerial classification of the Catalogue of Life.

* ~3 names per taxon, examples: like "Puma concolor", "Felis concolor" etc
  - finding all information about species is hard, because of changing names
* Hard to find a paper in BHL by having a citation (especially automatically)
  - not enough meta information
  - metadata problems: year, page, volume information are "strings", meaning they need to be parsed
    to compare with numbers
  - sometimes metadata is misleading (example?) missing
  - citations parsing is hard
  - inconsistent journal abbreviation and naming in different sources
* Hard to find nomenclatural events from name and citation
  - citation look above
  - name: OCR errors can change name,
  - name might exist but on a different page (like book index etc...)
  - name: annotations (sp.nov.,  comb. nov etc are not consistent)
  - name: abbreviated name problem (not solved yet)

* Solution to these problems
  * use COL data that connects name-strin to ref.
  * use CoL accepted/synonym information to get connect names-string to taxon
  * use name index in BHL together with COL data to solve these 3 problems.

* BHLnames project tries to solve these problems using aforementioned stuff

# Project description


Title: BHLnames

Study area description: Biodiversity Informatics

Design description: This is the whole paper actually (?)

## Goals

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


