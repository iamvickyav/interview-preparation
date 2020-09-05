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

```
> bin/solr delete -c <collection_name>
```

## DataImport from MySQL

**solrconfig.xml**
```xml
<requestHandler name="/dataimport" class="org.apache.solr.handler.dataimport.DataImportHandler">
    <lst name="defaults">
      <str name="config">data-config.xml</str>
    </lst>
</requestHandler>
```

**solrconfig.xml**
```xml
<lib dir="${solr.install.dir:../../../..}/dist/" regex="solr-dataimporthandler-.*\.jar" />
<lib dir="${solr.install.dir:../../../..}/dist/" regex="mysql-connector-java-8.0.21.jar" />
```

Reference: [Solr Tutorial](https://factorpad.com/tech/solr/reference/solr-delete.html)

* https://cwiki.apache.org/confluence/display/solr/DataImportHandler

* https://gist.github.com/rnjailamba/8c872768b136a88a10b1

* https://medium.com/@ersinilyazi/import-data-from-mysql-database-in-apache-solr-8-2-with-dataimporthandlers-e1d8c9b06380
