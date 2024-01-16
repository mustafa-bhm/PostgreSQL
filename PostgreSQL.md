list all databases in psql  
```console
~ psql
 \l 
```
CREATE  A DATABASE  
```console
CREATE DATABASE test;
```
Connect to a specific local database named "test" (Option 1)
```console
 psql -h localhost -p 5432 -U mac test
```
Connect to a specific local database named "test" (Option 2 ) 
```console
 \l
 \c test --(this is the name of the database )
```
Delete a Databse 
```console
DROP DATABASE test;
```
Create Table
```console
CREATE TABLE table_name (
    Column name + data type + constrains if any 
)
```
Example of table 
```console 
CREATE TABLE person(
    id int,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    gender VARCHAR(6),
    date_of_birth TIMESTAMP,
)
```

list tables in a Database
```console
~psql
\c <database_name>
\d
```
Access a specific table in a database
```console
~psql
\c <database_name>
\d <table_name>
```
Delete/Drop a table 
```console
DROP TABLE <table_name>
```
Create a table
```console
test=# CREATE TABLE person (
test(# id INT,
test(# first_name VARCHAR(50),
test(# last_name VARCHAR(50),
test(# gender VARCHAR(7),
test(# date_of_birth DATE);

```
Create a table with Constraints 
```console
test=# CREATE TABLE person (
test(# id BIGSERIAL NOT NULL PRIMARY KEY,
test(# first_name VARCHAR(50) NOT NULL,
test(# last_name VARCHAR(50) NOT NULL,
test(# gender VARCHAR(50) NOT NULL,
test(# date_of_birth DATE NOT NULL,
test(# email VARCHAR(150) );

```
Insert into a table
```console
test=# INSERT INTO person (first_name, last_name, gender, date_of_birth)
test-# VALUES ('Anne', 'Smith', 'FEMALE', date '1988-01-09');
```
Inject data from sql file 
```console
\i /Users/mac/projects/.../person.sql

```
Order by <column_name> ASC
```console
SELECT * FROM person ORDER BY country_of_birth ;
```

Order by <column_name> DESC
```console
SELECT * FROM person ORDER BY country_of_birth DESC ;
```
Select <column_name> and remove duplicat
```console
 SELECT DISTINCT country_of_birth FROM person ORDER BY country_of_birth ;
```

Where Clause and AND 
```console
SELECT * FROM person WHERE gender = 'Female';

SELECT * FROM person WHERE gender = 'Female' AND country_of_birth = 'Poland';
```