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


<!-- vim-markdown-toc GFM -->

* [Abstract](#abstract)
  * [Background](#background)
  * [New information](#new-information)
* [Keywords](#keywords)
* [Classifications](#classifications)
  * [Taxon Classification](#taxon-classification)
  * [Subject classification](#subject-classification)
* [Funder](#funder)
* [Introduction](#introduction)
* [Project description](#project-description)
  * [Goals](#goals)
  * [Technical introduction](#technical-introduction)
  * [Architecture](#architecture)
    * [Dependencies](#dependencies)
  * [Workflow](#workflow)
    * [Preprocessed data for Naive Bayes classifier](#preprocessed-data-for-naive-bayes-classifier)
    * [Initialization and data import](#initialization-and-data-import)
    * [Configuration file creation](#configuration-file-creation)
    * [Database and cache initialization](#database-and-cache-initialization)
      * [Year processing](#year-processing)
      * [Page and volume number processing](#page-and-volume-number-processing)
      * [Scientific names processing](#scientific-names-processing)
      * [Calculation of a taxonomic statistic](#calculation-of-a-taxonomic-statistic)
      * [Normalization of the books' and journals' titles](#normalization-of-the-books-and-journals-titles)
      * [Nomenclatural annotations](#nomenclatural-annotations)
    * [Main functionality](#main-functionality)
      * [Taxonomic intelligence workflow](#taxonomic-intelligence-workflow)
      * [Nomenclatural references workflow.](#nomenclatural-references-workflow)
        * [Collecting "evidences" of a citation match](#collecting-evidences-of-a-citation-match)
        * [Making a decision](#making-a-decision)
      * [Arbitrary references workflow](#arbitrary-references-workflow)
    * [Finding](#finding)
  * [Interfaces](#interfaces)
    * [Input formats](#input-formats)
    * [GUI](#gui)
      * [Embeddable widget](#embeddable-widget)
      * [API](#api)
      * [Command line](#command-line)
  * [Audience](#audience)
    * [Examples of usages](#examples-of-usages)
    * [Summary of scores](#summary-of-scores)
    * [Benchmarks](#benchmarks)
    * [Open data deliverables](#open-data-deliverables)
  * [Conclusions](#conclusions)
* [Web location (URIs)](#web-location-uris)
* [Technical specification](#technical-specification)
* [Repository](#repository)
* [Usage license](#usage-license)
* [Implementation](#implementation)
* [Additional information](#additional-information)
* [Acknowledgements](#acknowledgements)
* [Author contributions](#author-contributions)
* [References](#references)
* [Figures](#figures)
* [Tables](#tables)
* [Supplementary material](#supplementary-material)
* [Endnotes](#endnotes)

<!-- vim-markdown-toc -->

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

1. Add "taxonomic intalligence" to the BHL's index of scientific names.

    Supplement the nomenclatural event index with CoL synonym data to optionally extend BHL name search to include all relevent taxonomical information by returning search results for the accepted name and all of its synonyms.

2. Link to original species descriptions and nomenclatural events in BHL.

    Use citation search in combination with CoL nomenclatural citations to build an nomenclatural event index that will increase usability of BHL for biodiversity researchers.

3. Dramatically simplify citation string search using the names index.

    Use citation metadata in combination with occurences of a scientific name to link to pages that potentially match the citation with a provided probability score.

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

The project requires installed PostgreSQL database.

Initialization phase of the project requires internet access to a data export from BHL (https://www.biodiversitylibrary.org/data/data.zip) and the BHLindex RESTful API.
Internet connection must be reasonably fast due to the large amount of downloaded data.

BHLindex is an Open Source application written in Go that creates a scientific names index of BHL.
The application scans BHL's 60 million pages, detects scientific names and provides data about their page location via RESTful interface. It is possible to use publicly available URL that serves BHLindex API at (LINK).

There are many dependencies on Go modules, some of them written specifically for Global Names project.
We will talk about some of GN modules further.
Go dependencies are required only during the compilation of the project and are not needed for running BHLnames service or commandline application.

## Workflow

BHLnames has 2 distinct steps. Initialization and service.
Initialization step requires remote access to BHL data dumps and to a RESTful API of BHLindex service.
Service step provides a user with a web-interface, RESTful API and comman-line application to get taxonomic details about names, match nomenclatural reference to a page in BHL, match a reference string to BHL pages.

### Preprocessed data for Naive Bayes classifier

In the program we use Naive Bayes algorithm for determining the most like candidates for citation matching.
This algorithm is based on collection of evidences that make References in BHL more or less likely candidates to a match with a citation.
For this algorithm to function we need to decide beforehand which evidences will be collected for each case and how much weight each of them has to influence the final decision.

To calculate such weights for all used types of evidence we manually went through 3500 citation detection cases, and partitioned them into correctly and incorrectly identified (REF). This data is saved into a JSON file and is stored statically inside of the BHLnames binary executable. The data allowed us to calculate weights for each of the evidence type.

### Initialization and data import

From BHL's dumped files BHLnames receives metadata about Titles, Items, Pages and Parts.
BHL term Titles includes entities that might contain one or more volumes, for example a book or a journal.
Items correspond to physical volumes; an Item can be a book, a volume of a journal etc.
Pages correspond to scanned and processed pages of an Item.
Parts are distinct entities inside of an Item. For example a scientific paper is a Part.
Metainformation from BHL allows to integrate scientific names detected in BHL corpus to the rest of the data.

BHLindex API provides data and metadata about scientific names detected in BHL corpus.
Each name's occurence is associated with Internet Archive identifiers for a volume and a page.
Also it contains location on a page, and results of verificaton process.
Verification process resolves the name, if possible to a taxonomic database, like Catalogue of Life, or provides information if a name reconciles to a name in some other resource registered for GNverifier service.

Reconciliation is a process of matching a name to its lexical variants.
Resolution allows to receive taxonomic information for a particular name: if a names is a synonym, what is currently accepted name for the taxon, what kind of classification is associated with the taxon.

### Configuration file creation

BHLnames requires an access to PostgreSQL database.
Also it needs to know where to find BHL datafiles and how to access BHLindex' RESTful API.
All this data has to be included into configuration file.
The file is created as $HOME/.config/bhlnames.yaml when BHLnames commandliine application is executed first time.
A user has to edit the file and enter database credentials. All other settings can be left at its default values.

After that the application is ready for initialization.

### Database and cache initialization

To begin the process of initialization BHLnames has to create all the tables for its PostgreSQL database and create its cache directory for downloaded and processed data.

The database (default name is "bhlnames") should already exist (be created by hand).
It does not matter if it does have some data already or if it is totallly empty.
BHLnames initialization process will remove all old data and create required tables from scratch.
Now the database is ready to import the new data.

The cache directory structure is located at the OS standard location.
On most Linux distributions it would be created at "$HOME/.cache/bhlnames".
In case if the directory exists already, old data will be removed, so it will not be able to interfere with the updated data.

Then the initialization step downloads all the relevant data from BHL download site and from RESTful BHLindex API interface, processes it, and saves the result into a relational PostgreSQL database.

From the BHL's downloaded data we use "title.txt", "item.txt", "page.txt",  and "part.txt" files.
The 'title.txt' file contains metainformation for Titles, for example journals or books.
The 'item.txt' contains information about Items, for example a particular volume of a journal or a book.
The 'page.txt' has metadata about pages in an Item.
The 'part.txt' provides metadata about Parts of an Item, for example about a scientific paper title, authors, start and end page etc.

During the import several data-fields require additional attention.
Such fields include data about years of publication, volume, page information.Much of the data about detected name-strings will also be processed.
The largest processing job is required for the Titles' titles, for example a title of a book, a name of a journal etc.
We use such titles extensively for the matching process, and they will be prepared for fast matchins as it is described further.

#### Year processing

There are several fields with year information in BHL metadata.

The "titles" have 'StartYear' and 'EndYear' fields corresponding to
beginning of a pubhlishing and the end of the publishing.
The "items" have 'Year' field corresponding to the date of publication. However, in practice' some "items" might span several years, if they contain
volumes of a journal rebound together.
The "parts" have a "Date" field, usually in a 'yyyy-mm-dd' format where "-mm" and "-dd" parts are optional.

The year of publication data can be extracted from all of these fields, however some, or all of these fields might be empty.
Is some rare occastions the "year fields" are contradictory.
To determine a year of publicaton for a particular name we check for
existence of a year information going order "part", "item", "title".
For example if we found that the page is inside of a "part", we use the "part's" date to determine a year.
If "title" information is used, the "EndYear" value becomes a year for a page, indicating that the page could not be published later than this year.
For some pages no year data exists.

#### Page and volume number processing

Page number is an important field for connecting name occurance with the publication metadata, however the "PageNumber" field in "page.txt" cannot always be easily converted to an integer.
The value of the field is not always numeric, to name a few:

```
(1966, v.15, No.15)
, fig. A-B
, p. 431-436
, xiii-xiv
18 (Tab. XXXVII, XXX
208, Fig. 3
```

The page number is converted to an integer where possible.

The Volume information more often than not is not numeric; for example:

```
10, n. 20
Armitage, W.H.
v.2, pt. 1
(2020: Mar.)
0007
v.58:pt.1 (1889)
v.8:no.21 (2004:Apr)
```

We store volume data as is, without conversion to an integer.

#### Scientific names processing

More often than not a scientific name appears more than once in a volume.
To decrease the amount of noise we check if a page where name is found
is included into a "part", for example a scientific paper.
If yes, only the first occurance of a name in the "part" is included.
If a name is also detected in an "item", for example a journal volume, but is not part of any known "part", the first instance of a name in an "item" is included.
If there no "parts" are assigned to an "item", only the first appearance of a name in an "item" is included.

Every name string that is reconciled to a name in the Catalogue of Life (61.8% of all verified names) is associated with taxonomic resolution of a name-string to a clade in the Catalogue of Life.
For example, "Felis concolor" name-string is associated with a species clade where currently accepted name is "Puma concolor" according to the Catalogue of Life.

#### Calculation of a taxonomic statistic

Having most of the name-strings reconciled to the Catalogue of Life allows to calculate major kingdom and major clade appeared in BHL "items".
All such names contain their placement in the managerial Catalogue of Life classification.
This placement allows us to find out distribution of such names between kingdoms of the classification.

We are also able to find which clade in the classification contains more than
50% of all names resolved to the Catalogue of Life. To calculate it, we find how the names are distributed over each of "kingdom", "phylum/domain", "class", "order", "family".
Knowing the total number of names for each clade, we calculate the percentage for each clade, and pick one that contains more than 50% of all such names.
For example a book about Wolf Spiders would have more than 50% of all CoL names in the order of "Lycosidae".

Taxonomic statistics allows to find out a biological "theme" for the most of BHL volumes.

#### Normalization of the books' and journals' titles

BHL's "title.txt" contains a "FullTitle" field.
This field contains the full title of a journal or a book.
Citations of scientific publications almost always contain a title of a journal, so this field is very useful for matching a citation and a BHL Title.
However titles in citations are usually abbreviated, and the same title can have a large lexical variants where words are shortened or omitted in a hardly predictable way.
Fuzzy matching in this circumstances would be very time-consuming and would produce unreliable results.
Moreover, citation's title is in the middle of other information and to extract it as a separate entity is also very hard task.

For example, citation "Kirschstein, W. In: Verh. bot. Ver. Prov. Brandenb. 48:50. (1907)." contains abbreviated title to "Verhandlungen des Botanischen Vereins für die Provinz Brandenburg.".
Taking in account that citations often come from different sources and title abbreviations are not standardised, matching the citation to the title rarely succeeds.
In this manuscript we tried a new apprach that seems to be working quite well
for matching a citation to a journal title.

We made two observations.
First, that no matter how much a title is shortened, the first letter of the words have a tendency to survive.
Second, some words tend to be discarded from a shortened version alltogether.
Like in the example below "des", "für" and "die" words are totally discared from the shortened version of a title "Verh. bot. Ver. Prov. Brandenb".

We went through three thousand pairs of journal titles and their abbreviated counterparts.
We extracted words that are often get removed from shortened titles (TODO link to https://github.com/gnames/bhlnames/blob/master/io/dictio/data/excluded.txt).
Furthe we call these words "excluded".

Then we created 2 "fingerprints" for each title in BHL.
First "fingerprint" contains the first letter of every word in a title.
For the second "fingerprint" we remove all "exlcuded" words from the title and
then take first letter of every word that left.
For example  "Verhandlungen des Botanischen Vereins für die Provinz Brandenburg." would be normalized to "vdbvfdpb" and "vbvpb" fingerprints.
The reason we created two fingerprints is an obervation that more often than not, the "excluded" words either stay in a citation intact, or are removed from a citation completely.

For our example we end up with the following fingerprints:

```
The Journal Title:
Verhandlungen des Botanischen Vereins für die Provinz Brandenburg.
vdbvfdpb, vbvpb

The Citation:
Kirschstein, W. In: Verh. bot. Ver. Prov. Brandenb. 48:50. (1907).
kwivbvpb
kwvbvpb
```

The second "fingerprint" from the journal title "vbvpb" is included into the second "fingerprint" of the citation "kw**vbvpb**".
Therefore we can assume that the citation contains the title of the journal.

Additional rules for fingerprint creatsion are:

* Journal titles with less than 3 words do not get "fingerprints" created.
* Word "and" and "&" both become "&".
* The "fingerprints" longer than 10 characters are truncated to the first 10 characters.

During the data import we create approximately 400,000 "fingerprints" from BHL Titles titles.
Understandably it would be very time consuming to find which fingerprints out
of these 400,000 are included into each citation.
Because of that we implemented an Aho-Corasick algorithm (REF, REF) that allows very fast pattern inclusion detection via a modification of a suffix tree approach.

All of the data generated for the Aho-Corasick algorithm during initializationis backed up to the BHLnames' cache directory.
When BHLnames starts again this data is read and loaded into the memory according to the Aho-Corasick algorithm.
In then can be used for a very fast queies that match citations to the titles recorded in BHL database.

#### Nomenclatural annotations

When BHLindex detects scientific names in BHL corpus, it also detects the presence of "nomenclatural annotations" in a vicinity of each name occurence.

Nomenclatural annotions differ slightly depending on a year of publication, exiting nomenclatural rules, and a personality of authors.
In addition optical character recognition omits or modifies some characters.
As a result we found a large variety of nomenclatural annotations in BHL texts.
Here are a few examples:

```
sp.nov
sp. nov."。
n, sp:
subsp nov.
ssp. nov.?
'sp. n.),
nov. comb)
n. sp;;
(nov. comb)
n. sp..»
sp. nov.'.
sp« n.
sp., 2n.),
|n. sp.].
nov. sp.(3),
n. sp.,375
n> sp>
nv. sp.
(n, sp,):
nv. sp.,
(sp?) n
(n. sp,?)
sp. nov,).
sp. (n=5).
sp. nov.228
subsp.' nov.,
,n. comb.;
sp. nov.557
n. sp.38
(n. comb,
nov. sp.121
^,sp. n.,
nov. subsp).
nov. sp.^)
```

We normalized all the variants into the following categories:

```
SP_NOV    - new species
SUBSP_NOV - new subspecies
COMB_NOV  - new combination
NO_ANNOT  - no nomenclatural annotation
```
### Main functionality

The BHLnames program helps to find answers to these three questions:

* Where BHL contains information about a taxon, given a name string that can be resolved to the taxon.
* Where is a page which corresponds to a given nomenclatural citation + a name-string.
* Where is a BHL page which corresponds to a given reference + a name-string.

#### Taxonomic intelligence workflow

A "taxonomic intelligence" workflow includes an input and output.
The input consists of one or more scientific name-strings.
The output provides information which taxon the name resolves to, what is the currently accepted name for the taxon according to the Catalogue of Life, provides a link to images of the taxon according to Encyclopedia of Life, describes sinonym names for the taxon.
Also it tells how many references include information about the taxon.
Then it provides list of references which include the taxon together with page links.

Every Reference also provides additional statistics about its Item. It tells how many unique name-strings were detected in the Item, What is the kindom that contains the majority of detected names, what is the smallest taxon that contains more than half of all detected names.

Reference here can be a Part, or Item. If Item contains the name inside of  Parts and outside of any Part, data is provided for the first detection of the taxon in each of these entities.

The main difference between this approach and search of BHL by name is that the search aggregates information about all mentions of a taxon in BHL, no matter what name associated with a taxon was detected. This approach allows to get data linked from all literature in BHL, no matter when it was published and independently on development of Taxonomic science.

Optionally, it is possible to limit the list of returned references to a particular name and avoid the expansion of search to all synonyms.

(TODO an example of output)

#### Nomenclatural references workflow.

Publications that contain nomenclatural events are especially valuable for taxonomists.
Such publications might contain description of new species, changes in names of species as a result of placing them in a different genus, changed rank, "promotion" of infraspecies to species etc.

BHLnames makes it possible to discover such publicatons in BHL by providing an input that consists of a name-string created in the publivcation and the citation of the publication.
It is helpful if such details about publicaton like the year of publication, volume and page numbers are given separately in their own fields.

(TODO Example of input in JSON)

##### Collecting "evidences" of a citation match

To be able to estimate how sure we are that we did find the page where a particular nomenclatural citation exists, we collect several pices of "evidence" that would provide as clues about validity of our assurance.

In natural language processing such evidences are often called "features", and, as a rule, none of these evidences are an iron-clad indicator of a success.
We have to collect several types of them and use calculated weights for each of the evidence to make the final judgement.
The Naive Bayes method assumes that all of these features have no influence on each other. And while some rule do influence each other, from the practical standpoint Naive Bayes classifiers work quite well in many cases.

Now we will describe the evidences we collect to make a decision.

1. Name-string matching

The first step after receiving an input is finding all the References that contain a requested name.
Such search is performed without synonymy, so it only contains References that contain the name-string.

2. BHL Title's title matching

In the next step the titles of the References are compared with provided citatons.
We used descirbed earlier title "fingerprints" for a fast matching of citations to the titles of BHL Titles (books, journals etc.).

3. Year matching

The algorithm tries to match the year of the input citation with the years of the found References.
Note that sometimes the year of BHL Reference is known only approximately, for example if there is only Titile's start and end of publication data are given. Sometimes there is no year information at all.
The algorithm takes in account not only exact matches of a year, but also cases where a Reference year is close to the provided year in the input.

3. Page numers, volume matching

We use heuristic algorithms to compare given year, volume, page numbers information to match them to References obtained during the first step.

4. Nomenclatural annotations

More often than not, papers describing new species would have a nomenclatural annotation like "sp. nov.", "comb. nov" etc.
We normalized annotations occured in BHL as described earlier.
If a name occurance contains such annotation, it is registered as another "evidendce" in favor that the Reference is the nomenclatural one from the citation.

##### Making a decision

Using precalculated weights for the described above "evidences" we derive a total matching score for each Reference.
After that we are able to sort the references by the score and decide if the top result has a score high enough for being classified as a possible occurance of the citation in BHL.

The value of the score allows us to state a probabiliby of cussessful citation detection in the BHL corpus.

#### Arbitrary references workflow

The workflow for finding of arbitrary refernces is quite similar to the detetection of nomenclatural references.
The input is identical, and collection of "evidences", scoring and decision making are almost the same.
The only difference is that we do not take in account nomenclatural annotations located in the vicinity of the name-string.

### Finding

## Interfaces

### Input formats

### GUI

#### Embeddable widget

#### API

#### Command line

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


