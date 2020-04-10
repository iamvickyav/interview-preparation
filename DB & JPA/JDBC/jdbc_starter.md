# Database connection from Java
## Table of Contents

  * [Concepts](#concepts)
    + [Java Database Connectivity (JDBC)](#java-database-connectivity--jdbc-)
    + [DataSource](#datasource)
    + [Connection](#connection)
    + [ConnectionPool](#connectionpool)
    + [Distributed Transaction](#distributed-transaction)
    + [Statement](#statement)
    + [PreparedStatement](#preparedstatement)
    + [SQL Injection Sample](#sql-injection-sample)
    + [How PreparedStatement improves performance over Statement](#how-preparedstatement-improves-performance-over-statement)
    + [ResultSet](#resultset)
    + [Closing a connection](#closing-a-connection)
  * [Must Read](#must-read)

## Concepts

### Java Database Connectivity (JDBC)

JDBC is an application programming interface (API) for the programming language Java, which defines how a client may access a database

### DataSource

An object has information such as the location of the database server, the name of the database, the network protocol to use to communicate with the server etc. Its the alternative for DriverManager class

### Connection

Physical connection to the database created using the DataSource.getConnection() method. Connection is closed once the query is executed. But its too costly to create every time. Hence come the ConnectionPool concept

### ConnectionPool

When application closes a pooled connection, the connection is returned to a pool of reusable connections. The next when connection is requested with getConnection, connection from the pool will be returned hence avoids creating a new physical connection every time. Improves performance

DataSource which implemented ConnectionPoolDataSource can support pooled connection

### Distributed Transaction

DataSource which implemented XADataSource can support distributed transaction (in EJB)

### Statement

Interface that represents a SQL statement. Connection object is needed to create a Statement object. Used to implement simple SQL statements with no parameters

Methods - execute, executeQuery, executeUpdate

### PreparedStatement

Preferred If we have to execute a Statement object many times

**How it works differenly than Statement ?**

PreparedStatement is given a SQL statement when it is created & sent to the DB where it is compiled. 

As a result, the PreparedStatement object contains not just a SQL statement, but a SQL statement that has been precompiled. This means that when the PreparedStatement is executed, the DBMS can just run the PreparedStatement SQL statement without having to compile it first

**Advantages**

* Precompilation and DB-side caching of the SQL statement
* Prevention of SQL injection attacks by builtin escaping of quotes and other special characters

Thumb Rule - Statement for DDL and PreparedStatment for DML

Methods
executeUpdate() for create, drop, insert, update, delete
executeQuery() for the select query

### SQL Injection Sample

**NOTE** If we don't use ? (question mark) PreparedStatement also is not safe from SQL Injection attacks

Statement
```
PreparedStatement stmt = conn.createStatement("INSERT INTO students VALUES('" + user + "')");
stmt.execute();
```

PreparedStatement
```
PreparedStatement stmt = conn.prepareStatement("INSERT INTO student VALUES(?)");
stmt.setString(1, user);
stmt.execute();
```

User Input
```
Robert'); DROP TABLE students; --
```

### How PreparedStatement improves performance over Statement

[Read here](https://stackoverflow.com/a/34126564)

### ResultSet

Represents the results from execution of Statement. Data in ResultSet is accessed using Cursor

### Closing a connection

Use close() method in Statement to release the resource. ResultSet objects also gets closed when close() is called


## Must Read

[JDBC Basics](https://docs.oracle.com/javase/tutorial/jdbc/basics/index.html)

[A guide to accessing databases in Java by marcobehler](https://www.marcobehler.com/guides/a-guide-to-accessing-databases-in-java#plain-jdbc)

[SQL Injection in sarcasm](https://xkcd.com/327/)


