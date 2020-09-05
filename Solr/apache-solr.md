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

## Deleting all entries from Solr
```sh
curl http://localhost:8983/solr/bookbazzar/update -H "Content-Type: text/xml" --data-binary '<delete><query>*:*</query></delete>'

curl http://localhost:8983/solr/bookbazzar/update --data '<commit/>' -H 'Content-type:text/xml; charset=utf-8'
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

**data-config.xml**

```xml
<dataConfig>
<dataSource type="JdbcDataSource" 
            driver="com.mysql.jdbc.Driver"
            url="jdbc:mysql://localhost:3306/book_bazzar" 
            user="root" 
            password="rootroot"/>
<document>
  <entity name="product"  
    pk="id"
    query="select id,name,language from products"
    deltaImportQuery="SELECT id,name,language from products WHERE id='${dih.delta.id}'"
    deltaQuery="SELECT id FROM products  WHERE updated_at > '${dih.last_index_time}'"
    transformer="RegexTransformer"
    >
     <field column="id" name="id"/>
     <field column="name" name="name"/> 
     <field column="language" name="language" splitBy=","/>       
  </entity>
</document>
</dataConfig>
```

**SQL DDL**

```sql
CREATE TABLE products (
    id int(11) NOT NULL AUTO_INCREMENT,
    updated_at timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    name varchar(163) DEFAULT NULL,
    language varchar(30),
    PRIMARY KEY (id)
);
```

Reference: [Solr Tutorial](https://factorpad.com/tech/solr/reference/solr-delete.html)

* https://cwiki.apache.org/confluence/display/solr/DataImportHandler

* https://gist.github.com/rnjailamba/8c872768b136a88a10b1

* https://medium.com/@ersinilyazi/import-data-from-mysql-database-in-apache-solr-8-2-with-dataimporthandlers-e1d8c9b06380
