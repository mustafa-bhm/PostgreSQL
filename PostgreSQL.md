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
