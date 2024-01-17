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

Select a a limited number of rows
```console
SELECT * FROM person LIMIT 10;
or 
SELECT * FROM person FETCH FIRST 10 ROWS ONLY;
```
IN keyword
```console
SELECT * FROM person WHERE country_of_birth IN ('China', 'Brazil', 'France');
```

BETWEEN
```console
SELECT * FROM person
WHERE date_of_birth 
BETWEEN '2023-01-01' AND '2023-05-01';
```


Filter rows by a Pattern using LIKE and ILIKE( which is not case sensitive)
(ex: select all rows where the email address ends with .com)
```console
SELECT * FROM person WHERE email LIKE '%.com';
or 
SELECT * FROM person WHERE country_of_birth LIKE 'P%';

SELECT * FROM person WHERE country_of_birth ILIKE 'p%';
```

GROUP BY ( this will count # of persons and group them  by country_of_birth)
```console
 SELECT country_of_birth, COUNT(*)  FROM person GROUP BY country_of_birth;
```

HAVING ( in this case we selected countries that have more than 5 persons)
```console
test=# SELECT country_of_birth, COUNT(*)
test-# FROM person
test-# GROUP BY country_of_birth
test-# HAVING COUNT(*) > 5
test-# ORDER BY country_of_birth;
```

MIN , MAX ( Select most or less expensie car )
```console
SELECT MAX(price) FROM car;
SELECT MIN(price) FROM car;
```

AVG
```console
SELECT AVG(price) FROM car;
or
SELECT ROUND(AVG(price)) FROM car;
```

Select min price for a car make and model
```console
test=# SELECT make, model, MIN(price) FROM car
test-# GROUP BY make, model;

  make      |          model          |   min    
---------------+-------------------------+----------
 Toyota        | Land Cruiser            | 20644.10
 Mercedes-Benz | S-Class                 | 76728.03
 BMW           | M6                      | 73400.59
 Kia           | Amanti                  | 45082.30

test=# SELECT make, MIN(price) FROM car
GROUP BY make;

 make      |   min    
---------------+----------
 Ford          | 10406.22
 Smart         | 33563.75
 Maserati      | 38278.54
 Dodge         | 10407.30
 Infiniti      | 16511.07


test=# SELECT make, MIN(price) FROM car
GROUP BY make ORDER BY MIN(price);
  make      |   min    
---------------+----------
 Chevrolet     | 10160.67
 Jaguar        | 10257.62
 Nissan        | 10402.73
 Ford          | 10406.22
 Dodge         | 10407.30
```

Sum the price by make 
```console
SELECT make,  SUM(price) FROM car GROUP BY make;
 make      |    sum     
---------------+------------
 Ford          | 4085953.12
 Smart         |   33563.75
 Maserati      |  187894.59
 Dodge         | 2762150.54
 Infiniti      |  280634.26
 MINI          |   75463.84
 Bentley       |  181238.44
 
```