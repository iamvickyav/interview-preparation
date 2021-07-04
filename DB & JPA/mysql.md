# MySQL Session

## Query

### Database

```sql
CREATE DATABASE shopping;

USE shopping;

SHOW databases;
```

### DDL - Data Definition Language - Type of SQL Query

CREATE, ALTER, DESCRIBE

```sql

CREATE TABLE customer (cust_name VARCHAR(20));

DROP TABLE customer;

CREATE TABLE customer (
cust_id INT AUTO_INCREMENT, 
cust_name VARCHAR(20),
PRIMARY KEY (cust_id));

ALTER TABLE customer MODIFY cust_name VARCHAR(100);

DESCRIBE customer

ALTER TABLE customer MODIFY cust_name VARCHAR(100);

ALTER TABLE customer ADD cust_city VARCHAR(20);

ALTER TABLE customer DROP cust_city;

ALTER TABLE customer ADD cust_country VARCHAR(20) DEFAULT 'India';

-- Added Empty value as DEFAULT
ALTER TABLE customer ADD cust_city VARCHAR(20) NOT NULL;

-- Added 0 as DEFAULT
ALTER TABLE customer ADD cust_pincode INT NOT NULL;

TRUNCATE TABLE customer;


```

### DML

```sql
INSERT INTO customer (cust_name, cust_country, cust_city, cust_pincode)
VALUES ('Keerthana', 'India', 'Chennai', 610002), ('Vijay', 'India', 'Trichy', 642852);

UPDATE customer SET cust_city = 'Trichy' WHERE cust_id = 2; 
```
