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