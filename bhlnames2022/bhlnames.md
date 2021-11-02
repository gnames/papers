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
* Global Names exists
  - exists since ? 2004
  - consists of ZooBank, names tools (finder, parser, verifier)
  - covers lexical layer, connects via data-sources like CoL, IPNI, ZooBank to nomenclatural/taxonomy layers
* BHL exists
  - exists since 2006?
  - International effort
  - 90 mil pages, 270k volumes
  - Biological inormation exposed via names.
* BHL index made using Global Names tools
  - 12 hours to generate index 
  - Continuous improvemnt through improvement of algorithms and OCR
  - helps to find data
  - helps to find "biogroup" of every volume with names
  - Uses col management classification to augment data

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


