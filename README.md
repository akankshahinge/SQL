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
Constraints are used to specify rules for data in a table. This ensures the accuracy and reliability of the data in the table.
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
## Constraints Types
1. NOT NULL: Ensures that a column cannot have a NULL value
2. UNIQUE: Ensures that all values in a column are different
3. PRIMARY KEY: A combination of a NOT NULL and UNIQUE
4. FOREIGN KEY: Prevents actions that would destroy links between tables (used to link multiple tables together)
5. CHECK: Ensures that the values in a column satisfies a specific condition
6. DEFAULT: Sets a default value for a column if no value is specified
7. CREATE INDEX: Used to create and retrieve data from the database very quickly

## SQL Commands
### Create Database
```
$ CREATE DATABASE testDB;
```
### Show Database
```
$ SHOW DATABASES;
```
### Drop Database
```
$ DROP DATABASE testDB;
```
### Create Table
```
$ CREATE TABLE customer (
ID int8 PRIMARY KEY,
NAME varchar(50) NOT NULL,
AGE int NOT NULL,
CITY char(50),
SALARY numeric
)
```
### Insert into Table
```
$ INSERT INTO customer (ID,NAME,AGE,CITY,SALARY)
VALUES 
(2,'RRR',28,'Nashik',12345678),
(3,'MMM',28,'Nashik',12345678);
```
### Update table
```
$ UPDATE customer SET NAME='SSSS', AGE=25 WHERE ID=1;
```
### Delete table
```
$ DELETE from customer WHERE ID=2;
```
### Alter Table - Add column, change column datatype, drop column
```
$ ALTER TABLE customer ADD service_years int;
$ ALTER TABLE customer ALTER COLUMN service_years TYPE VARCHAR(50);
$ ALTER TABLE customer DROP COLUMN service_years;
```
### Drop table
The DROP TABLE command deletes a table in the database
```
$ DROP TABLE customer;
```
### Truncate Table
The TRUNCATE TABLE command deletes the data inside a table, but not the table itself
```
$ TRUNCATE TABLE customer;
```
### Select
```
$ SELECT * from customer;
$ SELECT name from customer;
$ SELECT DISTINCT name from customer;   (get unique rows from name column)
```
### Where Clause
```
$ SELECT name FROM customer WHERE name='SSSS';
$ SELECT * FROM customer WHERE name='SSSS';
$ SELECT * FROM customer WHERE age=28 AND city='Nashik';
```
### Limit By clause 
```
$ SELECT * FROM customer
ORDER BY name ASC
LIMIT 2;   
```
### Order By clause - ASC, DESC
```
SELECT * FROM customer
ORDER BY name ASC; 
```
### Functions in SQL
1. System defined: round(), upper(), lower(), count(), sum(), max(), substring(), concat(), trim(), replace()
   ```
   $ SELECT SUBSTRING(first_name, 1, 4) from customer;
   ```
2. User defined: Define your own functions

### Aggregate Functions
```
$ SELECT COUNT(name) FROM customer;
$ SELECT COUNT(*) FROM customer;
$ SELECT SUM(age) FROM customer;
$ SELECT round(AVG(age),2) FROM customer;
```
### Group By, Order By, Having clause
The WHERE clause places conditions on the selected columns, whereas the HAVING 
clause places conditions on groups created by the GROUP BY clause
```
$ SELECT customer_id, SUM(amount) AS total
from payment
GROUP BY payment_mode
ORDER BY total ASC

$ SELECT payment_mode, COUNT(amount) AS total
from payment
GROUP BY payment_mode
HAVING COUNT(amount)>=3
ORDER BY total DESC
```
### Order of execution
- In a SQL query, the order of execution is: FROM, WHERE, GROUP BY, HAVING, SELECT, DISTINCT, ORDER BY, LIMIT. 
Explanation:
1. FROM: First, the tables are specified and joined based on the JOIN clause. 
2. WHERE: Next, rows are filtered based on the conditions specified in the WHERE clause. 
3. GROUP BY: After filtering, rows are grouped together based on the specified columns. 
4. HAVING: Groups are further filtered based on conditions using the HAVING clause. 
5. SELECT: The columns to be retrieved are specified in the SELECT clause. 
6. DISTINCT: If specified, only unique rows are returned. 
7. ORDER BY: The result set is sorted based on the specified columns. 
8. LIMIT: Finally, the number of rows to be returned is limited using the LIMIT clause. 
- Key points to remember:
* The WHERE clause filters rows before grouping occurs. 
* The HAVING clause is used to filter groups created by the GROUP BY clause. 
* The ORDER BY clause sorts the final result set. 
* The LIMIT clause restricts the number of rows returned

### Timestamps Function
• SHOW TIMEZONE
• SELECT NOW()
• SELECT TIMEOFDAY()
• SELECT CURRENT_TIME
• SELECT CURRENT_DATE

### Extract Function
The EXTRACT() function extracts a part from a given date value.
Syntax: SELECT EXTRACT(MONTH FROM date_field) FROM Table
 • YEAR
 • QUARTER 
 • MONTH
 • WEEK
 • DAY
 • HOUR
 • MINUTE
 • DOW–day of week
 • DOY–day of year
```
$ SELECT EXTRACT(MONTH FROM payment_date) AS month
FROM payment
```
### Joins
Inner join (INNER JOIN), left join (LEFT JOIN), right join (RIGHT JOIN), full outer join (FULL OUTER JOIN)
```
 SELECT *
 FROM customer AS c
 INNER JOIN payment AS p
 ON c.customer_id = p.customer_id
```
### Self Join
Join table on itself
```
SELECT * FROM employee as T1
JOIN employee as T2
ON T1.empoyee_id = T2.manager_id
```
### Union
The SQL UNION clause/operator is used to combine/concatenate the results 
of two or more SELECT statements without returning any duplicate rows and 
keeps unique records
 To use this UNION clause, each SELECT statement must have
 • The same number of columns selected and expressions
 • The same data type and
 • Have them in the same order
```
SELECT cust_name, cust_amount from custA
UNION
SELECT cust_name, cust_amount from custB
```
### Union All
In UNION ALL everything is same as UNION, it combines/concatenate two or more table but keeps all records, including duplicates
```
SELECT cust_name, cust_amount from custA
UNION ALL
SELECT cust_name, cust_amount from custB
```
### SubQuery
```
SELECT *
FROM payment
WHERE amount > (SELECT AVG(amount) FROM payment)
```
```
SELECT customer_id, amount, mode
from payment
where customer_id IN (SELECT customer_id FROM customer)
```
```
SELECT first_name, last_name
FROM customer c
WHERE EXISTS (SELECT customer_id, amount
FROM payment p
WHERE p.customer_id = c.customer_id
AND amount >100)
```





