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

biodiversity informatics, global names, nomenclature, taxonomy, scientific names, parser, PEG

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

Tile: GNparser

Study area description: Biodiversity Informatics

Design description:

## Goals

The goals for GNparser stayed the same for Ruby, Scala and Go implementations:

1. High Quality.
   A parser should be able to break names into their semantic elements to the same standards that can be achieved by a trained nomenclaturalist or better.
   This will give users confidence in the automated process and allow them to set aside tedious and expensive manual parsing.

2. Global Scope.
   A parser should be able to parse all types of scientific names, inclusive of the most complex name-strings such as hybrid formulae, multi-infraspecific names, names with multilevel authorships and so on.
   No name-strings should be left unparsed, otherwise biological information attached to them may remain undiscoverable.

3. Parsing Completeness.
   All information included in a name-string is important, not just the canonical form of the scientific name.
   Authorship, year, rank information allow us to distinguish homonyms, similar names, synonyms, spelling mistakes, or chresonyms.
   Access to such information improves the performance of subsequent reconciliation (the mapping of all alternative name-strings for the same taxon against each other).
4. Speed.
   Users, especially large-scale aggregators of biodiversity data, are more satisfied with speedy processing of data as it allows them to move forward to more purposeful value-adding tasks.
   Speed reduces the purchasing/operating costs of the hardware used for production parsing.
5. Accessibility.
   To be available to the widest possible audience, a parser should be released as a stand-alone program, have good documentation, be able to work as a library, to function as a command line tool, as a tool within a graphical interface, to provide a remotely accessiblle API.
6. Development community. The code of GNparser should be have jj

The previous version of GNparesr written in Scala was the closest to fulfil these goals.
However soon we found out that Go language in our case had crucial advantages over Scala.
We noticed that Go was much easier to learn and faster very easy to deploy.
The memory footprint for a running application changed from a gigabyte (Scala) to a few megabytes (Go).
We started to receive important Open Source contributions because the code was easier to understand and modify.
We found that a talanted developer without prior Go knowledge can start making big contributions to the project in a matter of weeks.
Several other GNA projects, such as name finding (GNfinder), name reconciliation and resolution (GNverifier) also migrated to Go.
Go version provided a significant boost in performance.
Moving to Go allowed us increas development speed about 5-fold, and removed dependency on a particular developer.
Go binaries are dramatically easier to install.
Because of that it was logical to make a complete rewrite of GNparser in Go.

## Technical introduction

This implementation of GNparser (as well as previous ones) heavily dependent on Parsing Expression Grammar (PEG) approach to parsing.
We discussed PEG in more details in the paper about Scala version of GNparser [TODO REF].

PEG provides recursive rules which resemble regular expression.
The parsing engine is written in a PEGs domain language and much easier to read and understand than pure Regular Expressions.

Here is an example of the


## Architecture

## Performance

## Usecases

## Discussion

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


