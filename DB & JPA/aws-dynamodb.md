# DynamoDB 

Amazon DynamoDB is a fully managed, serverless, key-value NoSQL database

##  DB Jargons

[This is a simplified version of the Reference documentation here](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.CoreComponents.html)

In DynamoDB, tables, items, and attributes are the core components. 

A table is a collection of items, and each item is a collection of attributes

**table** is a collection of data

**item** An item is a group of attributes that is uniquely identifiable among all of the other items. No limit on number of items per table. Consider it like ROW in RDBMS table. The maximum item size in DynamoDB is 400 KB

**attribute** is something that does not need to be broken down any further. Consider it like COLUMN in RDBMS table

## Accessing Data

Each item in the table has a unique id. Rest of the attributes are schemaless hence don't have to be defined beforehand

**Types of Primary Key**

* Partition Key (hash attribute)
* Partition Key & Sort Key (range attribute)

Partition key value is input to a hash function, whose output determines the partition in which the item is stored. All items with the same partition key value are stored together, in sorted order by sort key value

Primary key can be string, number, or binary (aka only scalar data supported).

**Secondary Indexes**

A secondary index lets you query the data in the table using an alternate key, in addition to queries against the primary key. We can create one or more secondary indexes on a table.

Global secondary index – Not using the table's Partition & Sort Key. Max 20 indexes possible

Local secondary index – Use table's partition key but different sort key. Max 5 indexs possible

## Operations

### Control Plane

* CreateTable
* DescribeTable
* ListTables
* UpdateTable
* DeleteTable

### Data Plane

**PartiQL**
A SQL-Compatible Query Language to perform CRUD operations

**Classic APIs**
* Creating Data
    * PutItem
    * BatchWriteItem – Writes up to 25 items to a table
* Reading Data
    * GetItem
    * BatchGetItem – Retrieves up to 100 items from one or more tables.
    * Query – Retrieves all items that have a specific partition key. You must specify the partition key value
    * Scan – Retrieves all items in the specified table or index
* Updating Data
    * UpdateItem – Modifies one or more attributes in an item.
* Deleting Data
    * DeleteItem – Deletes a single item from a table.
    * BatchWriteItem – Deletes up to 25 items from one or more tables.
* Transaction
    * TransactWriteItems
    * TransactGetItems

## Data Types

* String
* Number
* Binary
* List, a Map, or a Set

## Accessing Dyanamo From Python

Refer [Boto3](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/dynamodb.html) library

## Learn DB designing in DynamoDB

[Watch Here](https://www.youtube.com/watch?v=OfZgHXsYqNE&t=377s&ab_channel=EnlearAcademy)

## Other advantages

* DynamoDB supports TTL (Time to Live) for automatic deletion of items from table
* Uses Encryption at rest which encrypts data (AES-256). So unauthorized access to underlying hard disk won't reveal data
* Point-in-time Recovery (PITR) aka Backups
    * **EarliestRestorableDateTime**, can restore table to any point in time upto last 35 days
    * **LatestRestorableDateTime** can restore to 5 minutes before the current time





