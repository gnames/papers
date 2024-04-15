# Can we standardise name-reconciliaton via OpenRefine?

Global Names Verifier (GNv) offers a powerful, configurable, and fast way to reconcile scientific names. 
GNv software aggregates data from more than 100 datasets. Queries return currently accepted names along with information about where the information returned resides. 
It allows finding matches for names that historically had several suffixes, and can do fuzzy and partial matches.  
It sorts data by many factors to provide the best available results reliably.  
With a strong focus on software optimization, given the many available features, it can process 2000 names a second, making it one of the fastest services available.

Catalogue of Life, GBIF, TNRS, LifeMatch, NCBI, World Flora Online, GLOBI Nomer, WikiData and others provide their own tools for name reconciliation.
All these tools have their scope, design decisions, input and output formats.
It would be great for researches if all existing and future tools would be standardised.
Then moving from one resource to another would be as easy as changing a URL to another service.
However standardisation of all existing and future resources to a common interface would be a very hard task.
Some of them have no monetary, or programmatic means to modify their code, while others have more urgent priorities.
Some resources support a specific research path where adhering to a rigid standard might hinder their innovation.

Implementation of the OpenRefine protocol might solve many of standartization problems.
Some resources already have it implemented (WikiData, GNverifier, Bionomia, ...???)
To switch from from one resource to another one would literally just change to a different URL.
Many people already use OpenRefine for their other reconciliation needs, and incorporation of name-reconciliation would be very beneficial for them.
~~This solution has some challenges. For example, OpenRefine reconciles names one by one, as a result reconciliation is quite slow, however still reasonable for hundreds to thousands of names.~~
While basic reconciliation is standard by design, extended options have much flexibility.
Nevertheless, we think OpenRefine would be a significant step forward for standardization between name-reconciliation tools and those who use them.

Cite? (Sharif's paper?) Blog post? Link to repo where Reconcilication Service lives.
