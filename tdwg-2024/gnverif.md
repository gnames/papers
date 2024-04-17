# Can we standardise name-reconciliaton via OpenRefine?

Global Names Verifier (GNverifier) offers a powerful, configurable and fast way to reconcile scientific names. 
GNverifier software aggregates data from more than 100 source datasets. 
Queries return currently accepted names when provided in a dataset. 
It allows finding matches for names that historically had several suffixes, and can do fuzzy and partial matches.  
It sorts data by many factors to provide the best available results reliably.  
With a strong focus on software optimization, given the many available features, it can process 2000 names a second, making it one of the fastest services available.

Catalogue of Life, GBIF, TNRS, LifeMatch, NCBI, World Flora Online, GLOBI Nomer, WikiData and others provide their own tools for name-reconciliation.
All these tools have their scope, design decisions, input and output formats.
It would be great for researchers if all existing and future tools would be standardised.
Then moving from one resource to another would be as easy as changing the URL.
However standardisation of all existing and future resources to a common interface would be difficult.
Some of them have no monetary, or programmatic means to modify their code, while others have more urgent priorities.
Some resources support a specific research path where adhering to a rigid standard might hinder their innovation.

Implementation of the OpenRefine protocol might solve many of standardisation problems.
Some resources already have it implemented (e. g. WikiData, GNverifier see https://github.com/gnames/gnverifier/wiki/OpenRefine-readme).
Many people already use OpenRefine for their other reconciliation needs.
Incorporation of name-reconciliation would be very beneficial.
Basic reconciliation by itself, is standard by design and a big step forward. 
We do note that extended options have much flexibility which would then need standardization by a human.
We think OpenRefine would be a significant step forward for standardization between name-reconciliation tools and those who use them.
