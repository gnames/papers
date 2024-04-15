# Can SQLite be the most 'frictionless' solution for biodiversity data?

Biodiversity data exchange heavily depends on standards, such as DarwinCore, ABCD, Taxon Concept Schema, CoLDP etc.
Standards provide terms with defined semantic meaning as well as a structure (for example TCS v1, Darwin Core Archive) for data exchange.
One significant problem in data exchange is ability to ingest and export data from one format to another.
Data exchanged using Darwin Core Archive or Taxon Concept schema is inert, and not trivial to parse, query and reformat.

Most data-exchange formats are based on comma separated value, XML or JSON formats.
In such files data is 'inert' and requires parsing and importing before it can be queried.
We suggest to exchange data in 'active' queriable way using SQLite-based files.

SQLite is a lightweight database which is installed on almost all computers by default.
The SQLite creates database located in just one file, that can be easily exchanged and compressed.
Its fast database engine is able comfortably work with terabytes of data.
The developers of SQLite promised to keep binary and text versions of SQLite files backward compatibe up to the year 2050.
All popular programming languages have libraries to connect to SQLite database and operate with its data using SQL query language.
Library of Congres of the United States recommends using SQLite format together with XML and JSON as a data-archival solution.

Using SQLite for biodiversity data exchange can be an exciting new opprotunity, where data can be easily queried, imported and exported in a standard way.
No need to write parsers to access the data.
We at Species File Group expermiment with using SQLite to create a universal convertor, where SQLite database serves as an internal data storage.
Importers of Darwin Core Archive, CoLDP, Taxon Works, GlobalNames data can be written once and work seamlessly with exporters written for such formats.


# SQLite: A 'Frictionless' Solution for Biodiversity Data Exchange?

Biodiversity data exchange relies on established standards like Darwin Core, Taxon Concept Schema (TCS), and CoLDP etc.
Standards provide terms with defined semantic meanings and structures (e.g., TCS v1, Darwin Core Archive) for data interoperability.
A notable challenge is the complexity involved in the ingestion and exportation of data across various formats.
Traditionally, data in formats such as Darwin Core Archive or Taxon Concept Schema is 'inert', making it cumbersome to parse, query, and reformat.

Commonly standards are based on data-exchange formats such as Comma Separated Values,XML, or JSON.
As a result data is hard to analyze and query until it is parsed and imported into a database.
We propose a paradigm shift toward using 'active' queryable SQLite-based files for data exchange.

SQLite, a ubiquitous lightweight database system. 
It integrates a database into a single file, facilitating straightforward data exchange and compression.
Its robust engine efficiently manages terabytes of data, with the SQLite developers committing to maintaining backward compatibility of both binary and text file versions until 2050.
SQLite connectivity is supported by all popular programming languages.
The United States Library of Congress endorses SQLite alongside XML and JSON for data archival, attesting to its reliability and long-term utility.

Implementing SQLite for biodiversity data exchange presents an innovative approach, enabling direct data queries without the need for specialized parsers.
Our team at the Species File Group is developing a universal converter using SQLite as the core storage solution.
This system facilitates seamless interactions between importers of formats like Darwin Core Archive, CoLDP, and Taxon Works, and exporters for similar standards.
This model not only simplifies data handling but also ensures consistency and efficiency in biodiversity data management.

In conclusion, adopting SQLite could revolutionize biodiversity data exchange by reducing operational friction and enhancing data accessibility, promising a streamlined and universally compatible data management framework.
