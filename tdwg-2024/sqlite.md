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

Using SQLite for biodiversity data exchange can be an exciting new opprotunity, where data can be easily queried, imported and exported in a standard way.
No need to write parsers to access the data.
We at Species File Group expermiment with using SQLite to create a universal convertor, where SQLite database serves as an internal data storage.
Importers of Darwin Core Archive, CoLDP, Taxon Works, GlobalNames data can be written once and work seamlessly with exporters written for such formats.



