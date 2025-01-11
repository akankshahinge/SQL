# SQL

- SQL is Structured Query Language, is a programming language to interact with databases.
- SQL applications: CRUD
- SQL is case insensitive
- Suppose your column name is MAX(age) and you want to select this for AVG. Then it gives error as it considers two aggregation function one inside other - AVG(MAX(age)) so we use backtick to get the results.

  ```
  Eg: select AVG(`MAX(age)`)
  ```

### Comments
```
-- Single line comment
/* */ Multi line comment
```

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
 - YEAR
 - QUARTER 
 - MONTH
 - WEEK
 - DAY
 - HOUR
 - MINUTE
 - DOW–day of week
 - DOY–day of year
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
- It is like nested query or inner query. we make use of opeartor like IN or EXISTS
- Subquery can be use with these clause: select, from, where, having

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
### Case Statement Syntax
```
SELECT customer_id, amount,
 CASE
 WHEN amount > 100 THEN 'Expensive product'
 WHEN amount = 100 THEN 'Moderate product'
 ELSE 'Inexpensive product' 
END AS ProductStatus
FROM payment
```
### Case Expression syntax
```
SELECT customer_id,
CASE amount
 WHEN 500 THEN 'Prime Customer'
 WHEN 100 THEN 'Plus Customer'
 ELSE 'Regular Customer'
END AS CustomerStatus
FROM payment
```
### Windows Function
- Window functions applies aggregate, ranking and analytic functions over a particular window (set of rows).
- And OVER clause is used with window functions to define that window
1. Aggregate: SUM, AVG, MIN, MAX, COUNT
2. Ranking: ROW_NUMBER, RANK, DENSE_RANK, PERCENT_RANK
3. Value/Analytics: LEAD, LAG, FIRST_VALUE, LAST_VALUE

```
SELECT new_id, new_cat,
 SUM(new_id)  OVER( PARTITION BY new_cat ORDER BY new_id) AS "Total",
 AVG(new_id)  OVER( PARTITION BY new_cat ORDER BY new_id) AS "Average",
 COUNT(new_id)  OVER( PARTITION BY new_cat ORDER BY new_id) AS "Count",
 MIN(new_id)  OVER( PARTITION BY new_cat ORDER BY new_id) AS "Min",
 MAX(new_id)  OVER( PARTITION BY new_cat ORDER BY new_id) AS "Max"
FROM test_data
```
```
SELECT new_id, new_cat,
 SUM(new_id)  OVER( ORDER BY new_id ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING)  AS "Total",
 AVG(new_id)  OVER( ORDER BY new_id ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING)  AS "Average",
 COUNT(new_id)  OVER( ORDER BY new_id ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING)  AS "Count",
 MIN(new_id)  OVER( ORDER BY new_id ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING)  AS "Min",
 MAX(new_id)  OVER( ORDER BY new_id ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING)  AS "Max"
 FROM test_data
```
NOTE: Above we have used: “ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING” 
which will give a SINGLE output based on all INPUT Values/PARTITION (if used)
```
SELECT new_id, 
ROW_NUMBER() OVER(ORDER BY new_id) AS "ROW_NUMBER",
RANK() OVER(ORDER BY new_id) AS "RANK",
DENSE_RANK()OVER(ORDER BY new_id) AS "DENSE_RANK",
PERCENT_RANK() OVER(ORDER BY new_id) AS "PERCENT_RANK"
FROM test_data
```
```
SELECT new_id,
 FIRST_VALUE(new_id)  OVER( ORDER BY new_id) AS "FIRST_VALUE",
 LAST_VALUE(new_id)  OVER( ORDER BY new_id) AS "LAST_VALUE",  
 LEAD(new_id)  OVER( ORDER BY new_id) AS "LEAD",
 LAG(new_id)  OVER( ORDER BY new_id) AS "LAG"
 FROM test_data
```
To lead and lag by 2 values
```
SELECT new_id,
 LEAD(new_id, 2)  OVER( ORDER BY new_id) AS "LEAD_by2",
 LAG(new_id, 2)  OVER( ORDER BY new_id) AS "LAG_by2"
 FROM test_data
```
### Common Table Expression
- A common table expression, or CTE, is a temporary named result set created from a simple SELECT statement that can be used in a subsequent SELECT statement
- We can define CTEs by adding a WITH clause directly before SELECT, INSERT, UPDATE, DELETE, or MERGE statement.
- The WITH clause can include one or more CTEs separated by commas
- These results is not stored in the memory, and each time the query is ran it generates temporay results. Once cte is created immediately the select should be written o query it immediately as result as tempory 
  and not stored in memory.
  ```
   WITH my_cte AS (
   SELECT  *, AVG(amount) OVER(ORDER BY 
   p.customer_id) AS "Average_Price", 
   COUNT(address_id) OVER(ORDER BY 
   c.customer_id) AS "Count"
    FROM payment as p
    INNER JOIN customer AS c
    ON p.customer_id= c.customer_id
    )
    SELECT first_name, last_name
    FROM my_cte
  ```
Multiple CTEs can also be defined by just comma
##### Difference between CTE and SubQuery
- In subquery, we first write main query and then subquery and in CTE, we first wite the CTE and then main query. Thinking pattern is, for subquery - bottom to top and for CTE - its top to bottom.
- Big difference, subquery can be only used once in main query, where as CTE can be used multiple times in main query.
- CTE reduces redandant and increase readability, introduces modularity, reuseability
##### *Types of CTE*
1. Non-Recursive CTE - standlone, and nested CTE (one CTE inside other)
   ```
   Example of nested CTE
   with cte1 as
   (
   select ....
   from ....
   where ....
   ),
   cte2 as
   (
   select ....
   from cte1
   where ....
   )
   select ....
   from cte2
   where ....
   ```
3. Recursive CTE

##### Tip: order by cannot be used in subquerys, views, CTE, inline functions. So use order by in main query.

### LIKE Operator
```
SELECT * FROM Customers
WHERE CustomerName LIKE 'A%';
```
### NOT LIKE Operator
```
SELECT * FROM Customers
WHERE CustomerName NOT LIKE 'A%';
```
### LIKE and Wildcard
There are two wildcards often used in conjunction with the LIKE operator:
- The percent sign % represents zero, one, or multiple characters
- The underscore sign _ represents one, single character
  ```
  $ SELECT * FROM Customers
  WHERE CustomerName LIKE 'a%';
  ```
  ```
  $ SELECT * FROM Customers
  WHERE city LIKE 'L_nd__';
  ```
  ```
  $ SELECT * FROM Customers
  WHERE CustomerName LIKE 'a__%';
  ```
  The [] wildcard returns a result if any of the characters inside gets a match.
  Return all customers starting with either "b", "s", or "p":
  ```
  $ SELECT * FROM Customers
  WHERE CustomerName LIKE '[bsp]%';
  ```
  The - wildcard allows you to specify a range of characters inside the [] wildcard.
  ```
  $ SELECT * FROM Customers
  WHERE CustomerName LIKE '[a-f]%';
  ```
### NOT IN
```
SELECT * FROM Customers
WHERE City NOT IN ('Paris', 'London');
```
### NOT BETWEEN
```
SELECT * FROM Customers
WHERE CustomerID NOT BETWEEN 10 AND 60;
```
### IS NULL and IS NOT NULL
```
SELECT CustomerName, ContactName, Address
FROM Customers
WHERE Address IS NULL;
```
```
SELECT CustomerName, ContactName, Address
FROM Customers
WHERE Address IS NOT NULL;
```
### TOP and LIMIT
TOP used by Microsoft SQL server
LIMIT used vy My SQL, PostgreSQL
```
SELECT TOP 5 * FROM customer;
```
```
SELECT * FROM customer
LIMIT 5;
```
TOP can also be used with percent
```
SELECT TOP 50 PERCENT * FROM Customers;
```
### Concatenate Columns
In MySQL
```
$ SELECT CustomerName, CONCAT(Address,', ',PostalCode,', ',City,', ',Country) AS Address
FROM Customers;
```
### Exists
- The EXISTS operator is used to test for the existence of any record in a subquery.
- The EXISTS operator returns TRUE if the subquery returns one or more records.
  ```
  SELECT SupplierName
  FROM Suppliers
  WHERE EXISTS (SELECT ProductName FROM Products WHERE Products.SupplierID = Suppliers.supplierID AND Price < 20);
  ```
### ANY and ALL
The ANY operator:
- returns a boolean value as a result
- returns TRUE if ANY of the subquery values meet the condition
ANY means that the condition will be true if the operation is true for any of the values in the range.
```
SELECT ProductName
FROM Products
WHERE ProductID = ANY
  (SELECT ProductID
  FROM OrderDetails
  WHERE Quantity = 10);
```
```
SELECT ProductName
FROM Products
WHERE ProductID = ALL
  (SELECT ProductID
  FROM OrderDetails
  WHERE Quantity = 10);
```
### SELECT INTO
The SELECT INTO statement copies data from one table into a new table.
```
SELECT * INTO CustomersGermany
FROM Customers
WHERE Country = 'Germany';
```
Tip: SELECT INTO can also be used to create a new, empty table using the schema of another. Just add a WHERE clause that causes the query to return no data:
```
SELECT * INTO newtable
FROM oldtable
WHERE 1 = 0;
```
### INSERT INTO SELECT
- The INSERT INTO SELECT statement copies data from one table and inserts it into another table.
- The INSERT INTO SELECT statement requires that the data types in source and target tables match
```
INSERT INTO Customers (CustomerName, City, Country)
SELECT SupplierName, City, Country FROM Suppliers;
```
### CASE
```
SELECT OrderID, Quantity,
CASE
    WHEN Quantity > 30 THEN 'The quantity is greater than 30'
    WHEN Quantity = 30 THEN 'The quantity is 30'
    ELSE 'The quantity is under 30'
END AS QuantityText
FROM OrderDetails;
```
### IFNULL
The MySQL IFNULL() function lets you return an alternative value if an expression is NULL:
```
SELECT ProductName, UnitPrice * (UnitsInStock + IFNULL(UnitsOnOrder, 0))
FROM Products;
```
### Procedures
```
mysql> delimiter //

mysql> CREATE PROCEDURE citycount (IN country CHAR(3), OUT cities INT)
       BEGIN
         SELECT COUNT(*) INTO cities FROM world.city
         WHERE CountryCode = country;
       END//
Query OK, 0 rows affected (0.01 sec)

mysql> delimiter ;

mysql> CALL citycount('JPN', @cities);
```
### Tricky MySQL queries
1. Get records for even ID (Use MOD fucntion)
   ```
   select DISTINCT CITY from STATION where MOD(ID,2)=0;
   ```
2. Substraction
   ```
   select (count(CITY) - count(DISTINCT CITY)) from STATION;
   ```
3. Names staring with aeiou
   ```
   SELECT DISTINCT CITY FROM STATION WHERE CITY LIKE 'A%' OR CITY LIKE 'E%' OR CITY LIKE 'I%' OR CITY LIKE 'O%' OR CITY LIKE 'U%
   ```
4. Regular Expression
   - ^ - starts with
   - $ ends with
   Select name which starts and ends with vowel
   ```
   SELECT DISTINCT CITY
   FROM STATION
   WHERE CITY REGEXP '^[aeiouAEIOU].*[aeiouAEIOU]$';
   ```
6. Select names where names does not start with vowels
   ```
   select DISTINCT CITY from STATION where CITY NOT REGEXP '^[aeiou].*$';
   ```
7. select names that dont end with vowel
   ```
   select DISTINCT city from STATION where NOT city REGEXP '[aeiou]$';
   ```
   OR
   ```
   SELECT DISTINCT CITY
   FROM STATION
   WHERE LOWER(RIGHT(CITY, 1)) NOT IN ('a', 'e', 'i', 'o', 'u');
   ```
   Here RIGHT(CITY, 1) is used to extract one character from CITY name and LOWER will convert it to lowercase
8. Query the list of CITY names from STATION that do not start with vowels and do not end with vowels. Your result cannot contain duplicates.
   ```
   select DISTINCT city FROM station where city NOT REGEXP '^[aeiou]' and city NOT REGEXP '[aeiou]$'
   ```
9. Query the Name of any student in STUDENTS who scored higher than  Marks. Order your output by the last three characters of each name. If two or more students both have names ending in the same last three   
   characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID.
   - Tip: To extract the last three characters RIGHT(Name, 3)
   - Tip: To extract middle characters MID(Name, start_position, length)
   ```
   SELECT 
    Name
   FROM 
      STUDENTS
   WHERE 
      Marks > 75
   ORDER BY 
      RIGHT(Name, 3), 
      ID;
   ```
10. Query the greatest value of the Northern Latitudes (LAT_N) from STATION that is less than . Truncate your answer to  decimal places.
       ```
       select round(MAX(LAT_N),4) from STATION where LAT_N < 137.2345;
       ```
11. Example of Replace and cast and CTE
    ```
    WITH AdjustedSalaries AS (
    SELECT 
        SALARY, 
        CAST(REPLACE(CAST(SALARY AS CHAR), '0', '') AS UNSIGNED) AS AdjustedSalary
    FROM EMPLOYEES
    ),
    ActualAverage AS (
        SELECT AVG(SALARY) AS ActualAvg FROM EMPLOYEES
    ),
    AdjustedAverage AS (
        SELECT AVG(AdjustedSalary) AS AdjustedAvg FROM AdjustedSalaries
    )
    SELECT 
        CEIL(ABS(ActualAverage.ActualAvg - AdjustedAverage.AdjustedAvg)) AS ErrorAmount
    FROM ActualAverage, AdjustedAverage;
    ```






