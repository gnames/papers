# SQLite: A 'Frictionless' Solution for Biodiversity Data Exchange?

Biodiversity data exchange heavily depends on established standards, such as Darwin Core, Audiovisual Core, Taxon Concept Schema (TCS) etc.
Standards provide terms with defined semantic meaning, and structures (e.g. TCS v1, Darwin Core Archive) for data exchange.
A notable challenge is the complexity involved in the ingestion and exportation of data across various formats.
Data in formats such as Darwin Core Archive or TCS is 'inert', and requires an effort to parse, query, and reformat.

Most data exchange is based on CSV, XML or JSON, and needs to be parsed and imported to a database before it can be queried.
We propose a paradigm shift toward using 'active' queryable SQLite-based files for data exchange.

SQLite is a lightweight database which is installed on almost all computers by default.
It integrates a database into a single file, facilitating straightforward data exchange and compression.
Its robust engine able to manage terabytes of data.
SQLite developers are committed to maintaine backward compatibility of both binary and text file versions until 2050.
The connectivity to the database is supported by all popular programming languages.
The United States Library of Congress endorses SQLite alongside XML and JSON for data archival, attesting to its reliability and long-term utility.

Implementing SQLite-based approach for biodiversity data exchange would enable direct data queries without the need for specialized parsers.
We at Species File Group expermiment with using SQLite to create a universal convertor, where SQLite database serves as an intermediate data storage.
In conclusion, we believe, that adopting SQLite for biodiversity data exchange can reduce operational friction, enhance data accessibility, promising a streamlined and universally compatible data management framework.
