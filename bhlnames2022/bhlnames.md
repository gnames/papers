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

The Catalogue of Life (CoL) project was established in 2000 with the goal of developing a global species checklist of all currently accepted scientific names [@Bisby2000; @Wilson2007].
As of this writing, CoL contains over 2 million accepted species.
CoL additionally tracks historical scientific names that are no longer accepted and contains 1.6 million of these synonyms, which enables finding species using either the currently accepted scientific name or their historical names.
Of the 3.7 million scientific names in CoL, 53% have nomenclatural references to the original species description in the literature.

Biodiversity Heritage Library (BHL) is the largest open access collection of biodiversity literature.
BHL was founded in 2005 to increase open access to biodiversity literature and is goverened by an internetional consortium [@Gwinn2009; @Rinaldo2009; @Smith2016; @Kalfatovic2019].
BHL currently comprises of 270 thousand volumes and 60 million pages of biodiversity texts.
By far the best way to discover biodiversity information in BHL is by searching for scintific names of organisms.
The index of scientific names for BHL is created by Global Names Architecture (GNA) project [@Costantino2020; @Richard2020].

The purpose of GNA is creation of services and tools that globally connect biodiversity information and research via scientific names.
GNA was founded in 2007 and includes nomenclatural (ZooBank, a zoological names registrator) and lexical tools (GNfinder, GNparser, GNverifier).
GNfinder detects scientific names in texts.
GNparser normalizes scientific name-strings and extracts semantic meanings of their components.
Normalizing scientific names also enables aggregating lexical variants of a name into a lexical group.
GNverifier enables searching for scientific names in more than 100 sources of biodiversity data, which helps verify whether the searched names string is a scientific name.
GNverifier uses data from Catalogue of Life, Encyclopedia of Life, Index Fungorum, Global Biodiversity Information Facility and many others.
These GNA tools are used for creating the scientific name index in BHL, which is used for BHL search [@Costantino2019; @Richard2020].

The BHL index of scientific names is created by processing BHL data through another GNA tool, BHLindex.
BHLindex breaks each volume into tokenized words, which enables the heuristic and natural language processing algorithms of GNfinder to detect potential scientific names within the volume's text.
Potential scientific names are verified (reconciled and resolved) via GNverifier.
The process of generating the BHL scientific names index has been highly optimized for performance, which enables processing 60 million BHL pages in ~12 hours on a modern laptop.
The speed of the BHL index creation offers the major advantage of being able to improve BHL search as the scanned page OCR improves [@Herrmann2020], and to incrementally improve the scientiifc name finding algorithms of GNA tools.
GNverifier also augments the metadata for each volume by attempting to determine the biological context.
Such information includes the kingdom which contains most of the names found in a volume, as well as the lowest clade that contains more than half of the volume' names.
The calculation uses the management classification from Catalogue of Life [@Gordon2009].

Searching for a specific scientific name in the BHL name index would often miss a significant amount of data due to changes in taxon names over time.
CoL currently contains ~3.6 million scientific names for ~2 million taxa.
The database of GNverifier contains 8 million scientific names, for ~2.5 million known taxa.
From this data we can estimate that there are 2-3 names per taxon on average, which fits with other published estimates (3.5 names/taxon in seed plants [@Scotland2003]).
To obtain more comprehensive knowledge about a biological species it is important to search not by just one scientific name, but by all synonyms used for the species historically.

Another way to aquire information from BHL is by searching for a particular paper.
Thanks to the BioStor project, metadata and page locations are known for 312,126 papers in BHL [@Page2010].
However, designing software to automatically find any paper in BHL by a citation is still challenging.
There are a large variety of lexical variants for every journal name (FIG).
No standard for citation formatting was ever agreed upon by publishers, so the arrangement of authors, year of publication, volume, issue, and page widely varies.
It is much easier to search for a year, volume and page data as numbers, but in BHL such metadata is stored as a string and is not consistent throughout the corpus with some journals using Roman numerals.
Quite often metadata is missing entirely or contains errors, which complicates linking citation strings to the correct page in BHL.

TODO: incorporate [@Pilsk2010] which covers librarian point of view on metadata
Pilsk, et al.: "Over the centuries, scientific nomenclature specialists have been forming species citations using abbreviations and notes that accommodate their spe- cial fields of study. These practices developed in an isolated manner specific to discipline (or subdiscipline) and independent of related species projects or the expertise of librarians and information professionals. Concurrently, librarians developing and implementing metadata policies and procedures never entered into conversation with taxonomists. Librarians did little to dis- cover how taxonomic citations are formed and what the actual access needs of the scientists were. As a result, each group adopted its own way of pro- cessing information, and constant translation between the two worlds was necessary. At best, a clumsy, but acceptable, disconnected reliance existed between these two fields"

TODO: Fig: examples of journal name different spellings

Even if a researcher has the citation for a nomenclatural event, it is often not a trivial task to navigate to the exact page in BHL in order to access the original species description for research.
Citations are hard to match to pages in BHL as described above.
Sometimes OCR errors change a name spelling and as a result exist in a volume under different spelling variants.

Quite often people add an annotation next to new species or combination, such as sp.nov, comb nov. However such annotations are not consistent (FIG), and also often modified by OCR.
When several species of the same genus are described, the genus in the name is often abbreviated, which also masks the name from a researcher.

TODO: Fig: examples for annotations

The project we describe in this paper helps to adress these problems with the following solutions:
1) BHLnames uses a combination of the names index, CoL data, and BHL metadata to improve nomenclatural and taxonomic search, link a citation to a page in BHL, or link to pages containing the original species description.
BHLnames uses CoL synonymy data to optionally expand name search to all its synonyms.
2) BHLnames normalizes BHL data for publication years and pages, making it easier to compare numeric representations.
3) The project uses 2,085,819 million citations of nomenclatural events for names in CoL to provide data about nomenclatural events.
4) BHLnames normalizes journal names in order to match citation strings to the journal name in BHL.
5) We use Naive Bayes approach to calculate probabilities of a citation to BHL page match and return the best results.
The data linking CoL nomenclatural citations to the original species description pages in BHL is downloadable from the Dryad data repository (Link).

# Project description


Title: BHLnames

Study area description: Biodiversity Informatics

Design description: This is the whole paper actually (?)

## Goals

The goals of BHLnames project are to:

1. Dramatically simplify citation string search using the names index.

    Use citation metadata in combination with occurences of a scientific name to link to pages that potentially match the citation with a provided probability score.

2. Link to original species descriptions and nomenclatural events in BHL.

    Use citation search in combination with CoL nomenclatural citations to build an nomenclatural event index that will increase usability of BHL for biodiversity researchers.

3. Add "taxonomic intalligence" to the BHL's index of scientific names.

    Supplement the nomenclatural event index with CoL synonym data to optionally extend BHL name search to include all relevent taxonomical information by returning search results for the accepted name and all of its synonyms.

(Methods)

## Technical introduction

BHLnames an Open Source project written in Go and JavaScript.
It can be freely used by anyone with Internet connection, write access to a PostgreSQL database, and XXX GB of disk space.
It consists of one stand-alone binary file and requires no additional dynamic libraries.
The file can be downloaded at: https://github.com/gnames/bhlnames/releases
Useage requires an initialization stage that can take several hours to complete, but afterwards the BHLnames binary can be used without an internet connection.

## Architecture

BHLnames' code structure mostly adheres to Clean Architecture principles [@Martin2018].
The main use-case functionality is defined in an interface (Link?).
The core (entity) modules that do not require input/output (I/O) interactions with a database, the internet or local storage, are located in the 'ent' directory.
The 'ent' directory also contains interfaces implemented by modules that need I/O access.
The Clean Architecture approach is advantageous because it uncouples core modules from particular implementations of external I/O processes and provides flexibility for changing ways of storing and accessing the data.
Modules requiring database, internet, user interfaces, or framework accesss implement entity interfaces and depend on the main use-case interface for providing functionality of BHLnames.
One exception to this rule is the 'bhlnames' directory that contains the commandline interface, following convention established by its Cobra module dependency.

BHLnames provides 3 user interfaces:

1. The commandline application starts and stops the web service or provides BHLnames functionality via the terminal.

2. The RESTful API provides endpoints for remote access to BHLnames functionality via HTTP calls.

3. The web interface is a Javascript widget that can be embedded on any website to connect scientific names with BHL literature in an interactive pop-up modal.

### Dependencies

Initialization phase of the project requires internet access to a data export from BHL (https://www.biodiversitylibrary.org/data/data.zip) and the BHLindex RESTful API.

BHLindex is an Open Source application written in Go that creates a scientific names index of BHL.
The application scans BHL's 60 million pages, detects scientific names and provides data about their page location via RESTful interface. It is possible to use publicly available URL that serves BHLindex API at (LINK).

There are many dependencies on Go modules, some of them written specifically for Global Names project.
We will talk about some of GN modules further.
Go dependencies are required only during the compilation of the project and are not needed for running BHLnames service or commandline application.

## Workflow

### Data Import

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


