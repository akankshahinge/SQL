# SQL

- SQL is Structured Query Language, is a programming language to interact with databases.
- SQL applications: CRUD

## SQL Commands
1. DDL (Data Definition Language): create, alter, drop
2. DML (Data Manipulation Language): select, insert, update and delete
3. DCL (Data Control Language): grant and revoke permission to users

## SQL Datatypes
- int: used for the integer value
- float: used to specify a decimal point number
- bool: used to specify Boolean values true and false
- char: fixed length string that can contain numbers, letters, and special characters
- varchar: variable length string that can contain numbers, letters, and special characters
- date: date format YYYY MM DD
- datetime: date & time combination, format is YYYY MM DD hh:mm:ss

## Primary key
- A Primary key is a unique column we set in a table to easily identify and locate data in queries
- A table can have only one primary key, which should be unique and NOT NULL
## Foreign Key
- A Foreign key is a field (or collection of fields) in one table, that refers to the PRIMARY KEY in another table.
- A table can have any number of foreign keys, can contain duplicate and NULL values
## Constraints
Constraints are used to specify rules for data in a table. This ensures the accuracy and reliability of the data in the table
Constraints can be specified when the table is created with the CREATE TABLE statement, or after the table is created with the ALTER TABLE statement
```
Syntax
CREATE TABLE table_name(
column1 datatype constraint,
column2 datatype constraint,
column3 datatype constraint,
....
);
```
