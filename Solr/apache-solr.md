# Apache Solr

Standalone Search Server
Lucene Search Library powers Indexing & Querying

## Documents

- Have Schema
- Composed of fields, fields have types

## Relevance

> Relavance = Term frequency \* inverse document freqency

Term Frequency - No of times a word seen in a doc divided by full count of all terms
Inverse Document Freqency - How often the term shows up in all documents

Found by log(count of docs in index/no of docs with that term)

Boost can be applied on top of relavance to make solr treat few field important than others

Score of doc = sum of all relavance

## Instructions

```sh
> bin/solr create_core -c films
```

```sh
> bin/post -c films example/films/films.xml
```

```sh
> http://localhost:8983/solr/films/schema/fields
```

```sh
> http://localhost:8983/solr/films/schema/copyfields
```

```sh
> bin/solr create_core -c solrhelp
```

```sh
> bin/post -c solrhelp -filetypes html https://factorpad.com/tech/solr/index.html
```

Reference: [Solr Tutorial](https://factorpad.com/tech/solr/reference/solr-delete.html)
