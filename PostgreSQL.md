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