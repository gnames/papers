---
title: Biodiversity Data Journal Template
author: John Doe, Jane Doe
date: 2021-10-27
csl: refs.csl
bibliography: refs.bib
geometry: margin=2cm
header-includes:
  - \hypersetup{colorlinks=false,
    allbordercolors={0.6 0.6 1},
    pdfborderstyle={/S/U/W 0.5}}
---

# Abstract

The GNparser is a biodiversity informatics application.
It allows to normalize various renderings of nomenlaturally equal scientific names ("**Homo sapiens sapiens** L." vs "**Homo sapiens (L.) ssp. sapiens** Linnaeus, 1753" for
example).
Also it allows to extract authors, year information, as well as to serve as a quality control for provided scientific name-strings.

The GNparser is an Open Source Go program created for the Global Names Architecture (GNA) initiaive.
It is the 3rd iteration of a parsing app/library from GNA.
It differs from previous approaches by unprecendented speed, higher quality of parsing, ability to be included as a native library by most popular programming languages.
It supports names from most biological codes based on binomial nomenclature: Zoological (ICZN), Botanical (ICN), Cultivar (TODO), Bacterial (TODO).

GNparser can be used as web-based program, via command line, and as a library.
The high perfomance of GNparser allows to process all scientific name-strings ever cretated in a matter of minutes.

## Background

Identifiers are a crucial tool used by humans thoughout the history to distinguishing objects, groups and ideas from each other.
Ones of the most successful and long-lived identifiers used in science are names of living organisms (scientific names).
Scientific names follow rules of binomial nomenclature, since Linnaeus (TODO REF).
They serve as universally accepted markers of biological taxa.
Scientific names are one of the most important metadata of biodiversity informatics.
The majority of historical and modern biological literature uses scientific names as the crucial tool to point to biological taxa.

Since its introduction in the middle of 18th century rules of binomial nomenclature streamlined communication about biological taxa.
They were one of the reasons of an explosion of biological discovery in the 19th century.
Scientific names preserved the legacy of 250 years of biodiversity knowledge accumulation until modern age.
They are the most important identifier to interconnect data from many resources.

However, the use of names sa identifiers is not straightforward for many different reasons.

1. A name can become obsolete
2. The taxon of a name can change its curcumscription. So the same name at different points of time might point to entities that differ.
3. If a taxon moved from one genus to another, its binomial name changes.
4. Lexical variants of a name are very common.

Scientific names parsers addresse the problem of lexical variants of names.
For humans it is relatively easy to deal with such variants, however for
automatic processing it is not a trivial task.


## New information

This is new

# Keywords

biodiversity, software

# Classifications

## Taxon Classification

Animalia, Plantae

## Subject classification

Bioinformatics

# Funder

Species File Group...

# Introduction

(Can have subsections)

Some background here  [@ICPN] trying to use a ref here. Some more refs
[@Kluyver2013;@ICZN;@ICTV] and then again ref [@ICPN;@FNA2002].

# Project description

Title:

Study area description: Earth

Design description:

Funding:

# Web location (URIs)

Homepage:

Wiki:

Download page:

Download mirror:

Bug database:

Mailing list:

Blog:

Vendor:

# Technical specification

Platform:

Programming language:

Operatin system:

Interface language:

Service endpoint:

# Repository

Type: Git

Browse URI:

Location:

Module:

Anonymous root:

# Usage license

MIT

# Implementation

Implements specification:

Audience:

# Additional information

# Acknowledgements

Thanks to you all

# Author contributions

# References

# Figures

# Tables

# Supplementary material

# Endnotes


