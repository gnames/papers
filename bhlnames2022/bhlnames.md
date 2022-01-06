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

Over the past 268 years, an estimated 2.5 million species have been named, described, and published in scientific journals by taxonomists around the world using the Linnaean classification system [@Linnaeus1753].
In order to describe new species it is imperative that taxonomists are able to quickly find and access past species descriptions to avoid re-describing an existing species with a new scientific name, and to hypothesize on how the new species is related to other species based on morphology and other characteristics.
The field of biodiversity informatics is still relatively young and there is still a huge backlog of work remaining to digitize past scientific literature, index the scientific names, and parse other unstructured scientific data from hundreds of years of past literature into a form that will be more usable for conducting research [@LeGuillarme2021].

Historically there has been a disconnect between the disciplines of biology and library science with different subdisciplines of taxonomy developing nomenclature and citation styles independently of one another and using non-standardized abbreviations that suited the specific needs of their subdisciplines, and librarians implementing metadata policies without conversing enough with biologists, resulting in suboptimal information systems that make it difficult and time consuming to efficiently conduct taxonomic research [@Pilsk2010].
Building a stronger collaboration between biologists, information scientists, and library scientists could help improve the of findability, accessibility, interoperability, and reusability (FAIR, [@Wilkinson2016]) of biodiversity knowledge which hopefully will help accelerate responding to emerging crises from climate change and biodiversity decline [@Urban2015].

Biodiversity Heritage Library (BHL) is the largest open access collection of biodiversity literature.
BHL was founded in 2005 to increase open access to biodiversity literature and is governed by an international consortium [@Gwinn2009; @Rinaldo2009; @Smith2016; @Kalfatovic2019].
BHL currently comprises of 270 thousand volumes and 60 million pages of biodiversity texts.
Perhaps the most common way to discover biodiversity information in BHL is by searching for scientific names of biological organisms.

The search index of scientific names for BHL was developed and is maintained by the Global Names Architecture (GNA) project [@Costantino2020; @Richard2020].
GNA was founded in 2007 with the aim of providing services and tools that globally connect biodiversity information and research via scientific names.
GNA includes nomenclatural (ZooBank, a zoological names registrar [@Patterson2010; @Krell2010; @Pyle2016]) and lexical tools (GNfinder, GNverifier, GNparser).
The GNfinder tool can be used to detect potential scientific names within text documents by searching for text patterns that follow the Linnaean nomenclature system [@Linnaeus1753].
GNverifier enables searching for scientific names in more than 100 sources of biodiversity data, which is used to help verify if potential scientific names found by GNfinder in text documents are actually scientific names.
GNverifier uses data from Catalogue of Life, Encyclopedia of Life, Index Fungorum, Global Biodiversity Information Facility and many others.
GNparser [@Mozzherin2017a] normalizes scientific names and extracts the semantic meanings of each component (FIG, @Mozzherin2017).
Normalizing scientific names also enables organizing lexical variants of a name into a lexical group.

A scientific name search tool, BHLindex, was developed through a 10 year collaboration between GNA and BHL [@Mozzherin2021].
BHLindex breaks each volume into tokenized words, which enables the heuristic and natural language processing algorithms of GNfinder to detect potential scientific names within a volume's text.
Potential scientific names are verified (reconciled and resolved) via GNverifier.
The process of generating the BHL scientific names index has been highly optimized for performance, which enables processing 60 million BHL pages in ~12 hours on a modern laptop.
The speed of the BHL index creation offers the major advantage of being able to continuously improve BHL search as the scanned page OCR improves [@Mozzherin2017; @Herrmann2020], and also allows incremental improvements to the scientific name finding algorithms of GNA tools.
GNverifier also augments the metadata for each BHL volume by attempting to  determine the kingdom and lowest clade that contain the most scientific names within a BHL volume using management classification from Catalogue of Life [@Gordon2009].

The Catalogue of Life (CoL) project was established in 2000 with the goal of developing a global species checklist of all currently accepted scientific names [@Reichhardt1999; @Bisby2000; @Wilson2007].
As of this writing, CoL contains over 2 million accepted species.
Searching in BHL for a biological organism using only its currently accepted scientific name could exclude a significant amount of information about the organism due to changes in taxon names over time.
CoL tracks historical scientific names that are no longer accepted and contains 1.6 million of these synonyms.
The database of GNverifier contains 8 million scientific names, for ~2.5 million known taxa.
From this data we estimate there are an average of 2 to 3 names per taxon, which fits with other published estimates (3.5 names/taxon in seed plants [@Scotland2003], but synonymy can vary by group with an estimate of only 1.2 names/taxon in stoneflies [@DeWalt2019]).
To obtain more comprehensive knowledge about a biological organism, it is important to search not by just one scientific name, but by all synonyms used in the literature for the organism historically.

Another way to access information in BHL is by searching for a particular paper.
Thanks to the BioStor project, metadata and page locations are known for ~310,000 papers in BHL [@Page2010; @Page2011].
However, designing software to automatically link to any paper in BHL by a citation string is still challenging.
There are a large variety of lexical variants for every journal name (FIG).
No standard for citation formatting was ever agreed upon by publishers, so the arrangement of authors, year of publication, volume, issue, and page widely varies.
It is much easier to search for a year, volume and page data as numbers, but in BHL numeric metadata is stored as a string and is not consistently formatted throughout the corpus with many journals in the past using Roman numerals.
Quite often metadata is missing entirely or contains errors, which complicates automatically linking citation strings to the correct page in BHL.
Of the 3.7 million scientific names in CoL, 53% have nomenclatural references to the original species description in the literature, and BHLnames attempts to automatically link to these citations in BHL.

TODO: Fig: examples of journal name different spellings

Even if a researcher has the citation for a nomenclatural event, it is often not a trivial task to navigate to the exact page in BHL in order to access the original species description for research.
Citations are hard to match to pages in BHL as described above.
Sometimes OCR errors change a name spelling and as a result exist in a volume under different spelling variants.

Quite often people add an annotation next to new species or combination, such as sp. nov., comb. nov. However such annotations are not consistent (FIG), and also often modified by OCR.
When several species of the same genus are described, the genus in the name is often abbreviated, which also masks the name from a researcher.

TODO: Fig: examples for annotations

The project we describe in this paper helps to adress these problems with the following solutions:
1) BHLnames uses a combination of the names index, CoL data, and BHL metadata to improve nomenclatural and taxonomic search, link a citation string to a page in BHL, or link to pages containing the original species description.
2) BHLnames normalizes BHL data for publication years and pages, making it easier to compare numeric representations.
3) The project uses 2,085,819 million citations of nomenclatural events for names in CoL to provide data about nomenclatural events.
4) BHLnames normalizes journal names in order to match citation strings to the journal name in BHL.
5) We use a Naive Bayes algorithm to calculate probabilities of a citation to BHL page match and return the best results.
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
BHL users [@Trei2016]
  Taxonomists
  Librarians
  Historians
  Citizen Scientists
  Nomenclators
  Artists
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


