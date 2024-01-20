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

List all Tables within a Database 
```console
\dt
 List of relations
 Schema |  Name  | Type  | Owner 
--------+--------+-------+-------
 public | car    | table | mac
 public | person | table | mac
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


Arithmetic Operations
```console
 SELECT  10+ 2;
 ?column? 
----------
       12
(1 row)

test=# SELECT 2^2;
 ?column? 
----------
        4
(1 row)

test=# SELECT 10 % 3;
 ?column? 
----------
        1
(1 row)

```
Arithmetic Operators (ROUND) [Calculate discount]
```console
SELECT id, make, model, price, price*.10 as discount FROM car;

 id  |     make      |          model          |  price   | discount  
------+---------------+-------------------------+----------+-----------
    1 | Ford          | Laser                   | 57789.93 | 5778.9930
    2 | Mercedes-Benz | GL-Class                | 83726.80 | 8372.6800
    3 | Hummer        | H3                      | 52793.25 | 5279.3250
    4 | Mitsubishi    | Montero                 | 55066.89 | 5506.6890
    5 | Geo           | Prizm                   | 40463.19 | 4046.3190


SELECT id, make, model, price,ROUND(price*.10, 2) as discount FROM car;

 id  |     make      |          model          |  price   | discount 
------+---------------+-------------------------+----------+----------
    1 | Ford          | Laser                   | 57789.93 |  5778.99
    2 | Mercedes-Benz | GL-Class                | 83726.80 |  8372.68
    3 | Hummer        | H3                      | 52793.25 |  5279.33
    4 | Mitsubishi    | Montero                 | 55066.89 |  5506.69


SELECT id, make, model, price,ROUND(price*.10, 2) as discount, 
ROUND(price-(price*.10),2) AS Discounted_Price FROM car;
id  |     make      |          model          |  price   | discount | discounted_price 
------+---------------+-------------------------+----------+----------+-----------------
    1 | Ford          | Laser                   | 57789.93 |  5778.99 |        52010.94
    2 | Mercedes-Benz | GL-Class                | 83726.80 |  8372.68 |        75354.12
    3 | Hummer        | H3                      | 52793.25 |  5279.33 |        47513.93
    4 | Mitsubishi    | Montero                 | 55066.89 |  5506.69 |        49560.20
```


COALESCE ( Set  default value , whne the value is null)
```console
SELECT email FROM person;
email                 
--------------------------------------
 gjellicorse0@sohu.com
 
 bstenton2@buzzfeed.com
 sfeetham3@topsy.com
 
 
 alevinge6@histats.com

SELECT COALESCE(email,'EMAIL NOT PROVIDED' ) FROM person;

 gjellicorse0@sohu.com
 EMAIL NOT PROVIDED
 bstenton2@buzzfeed.com
 sfeetham3@topsy.com
 EMAIL NOT PROVIDED
 EMAIL NOT PROVIDED
 alevinge6@histats.com
```

```console
SELECT NOW();
              now              
-------------------------------
 2024-01-18 19:29:59.165116-07
(1 row)

SELECT NOW()::DATE;
    now     
------------
 2024-01-18
(1 row)
```

Extract Year and month from Date 
```console
SELECT EXTRACT(YEAR FROM NOW());
 extract 
---------
    2024
(1 row)

SELECT EXTRACT(MONTH FROM NOW());
 extract 
---------
       1
(1 row)
```

Age Function 
```console
 SELECT first_name, last_name, date_of_birth, AGE(NOW(), date_of_birth) AS Age FROM person;
 first_name  |    last_name     | date_of_birth |               age               
--------------+------------------+---------------+---------------------------------
 Giorgi       | Jellicorse       | 2023-03-10    | 10 mons 4 days 14:46:48.561545
 Chaddie      | Clementet        | 2023-08-21    | 4 mons 24 days 14:46:48.561545
 Bruce        | Stenton          | 2023-03-06    | 10 mons 8 days 14:46:48.561545
 Susana       | Feetham          | 2023-02-14    | 11 mons 14:46:48.561545
 Brita        | Pinckney         | 2023-10-08    | 3 mons 6 days 14:46:48.561545
```

Delete a row 
```console
DELETE FROM person WHERE id=1;
DELETE 1
```
Update records
```console
UPDATE person SET email = 'susana@gmail.com' WHERE id = 4;

UPDATE person SET first_name = 'omar', last_name='Smith', email ='omar@gmail.com' WHERE id ='4';
```

Update Forign Key
```console
UPDATE person SET car_id = 1 WHERE id = 2;
```

Inner joins 
```console
SELECT * FROM person
JOIN car ON person.car_id = car.id;

 id | first_name | last_name | gender |      email      | date_of_birth | country_of_birth | car_id | id |    make    |  model   |  price   
----+------------+-----------+--------+-----------------+---------------+------------------+--------+----+------------+----------+----------
  2 | Omar       | Colmore   | Male   |                 | 1921-04-03    | Finland          |      1 |  1 | Land Rover | Sterling | 87665.38
  1 | Fernanda   | Beardon   | Female | fernandab@is.gd | 1953-10-28    | Comoros          |      2 |  2 | GMC        | Acadia   | 17662.69
```

LEFT JOINS

```console
SELECT * FROM person
LEFT JOIN car ON person.car_id = car.id;

id | first_name | last_name | gender |        email        | date_of_birth | country_of_birth | car_id | id |    make    |  model   |  price   
----+------------+-----------+--------+---------------------+---------------+------------------+--------+----+------------+----------+----------
  2 | Omar       | Colmore   | Male   |                     | 1921-04-03    | Finland          |      1 |  1 | Land Rover | Sterling | 87665.38
  1 | Fernanda   | Beardon   | Female | fernandab@is.gd     | 1953-10-28    | Comoros          |      2 |  2 | GMC        | Acadia   | 17662.69
  3 | John       | Matuschek | Male   | john@feedburner.com | 1965-02-28    | England          |        |    |            |          |         
(3 rows)


```

Export table as a CSV 
```console
 \copy (SELECT *FROM person LEFT JOIN car ON car.id = person.car_id) TO '/Users/mac/../results.csv' DELIMITER ',' CSV HEADER;
```