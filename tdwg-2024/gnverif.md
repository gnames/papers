# Can we standardise name-reconciliaton via OpenRefine?

Global Names Verifier is a powerful, configurable and fast way to reconcile scientific names. 
It allows to find matches for names that historically had several suffixes, can do fuzzy and partial matchses.
It aggregates data from more than 100 datasets, and shows currently accepted names, where such information is provided.
It sorts data by many factors, providing best available results reliably.
In spite of many available features it processes 2000 names a second, making it one of the fastests services available.

Catalogue of Life, GBIF, TNRS, LifeMatch, NCBI, World Flora Onlie, GLOBI Nomer, WikiData and others provide their own tools for name reconciliation.
All these tools have their scope, design decisions, input and output formats.
It would be great for researches if all existing and future tools had been standardised.
Then moving from one resource to another would be as easy as chaning a URL to another service.
However standartisation of all existing and future resources to a common interface would be a very hard task.
Some of them have no monetary, or programmatic means to modify their code, other have more urgent priorities.
Some resources follow their research path, and adhering to a rigid standard might hinder their innovation.

Implementation of OpenRefine protocol might solve many of standartization problems.
Some resources already have it implemented (WikiData, GNverifier, ...???)
Switching from one resource to another is literaly just chaning to a different URL.
Many people already use OpenRefine for their other reconciliation needs, and incorporation of name-reconciliation would be very beneficial for them.
This solution has its negative sides as well.
OpenRefine reconciles names one by one, as a result reconciliation is quite slow.
While basic reconciliation is standard by design, extended options have much flexibility.
Nevertheless, we thing OpenRefine would be a significant step forward towards the standardization of the scientific name-reconciliation tools.

