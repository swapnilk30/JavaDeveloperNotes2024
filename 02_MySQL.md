## What is a PRIMARY KEY ?

    The PRIMARY KEY constraint uniquely identifies each record in a table.
    Primary keys must contain UNIQUE values, and cannot contain NULL values.

    A table can not have more than one primary key.

    Rules for defining primary key:
        -two rows cant have the same primary key value.
        -the primary key field cannot be null.
        -the value in a primary key column can never be 
            modified or updated if any foreign key refers to that primary key.
        
## What is the FOREIGN KEY ?

    FOREIGN KEY is a column that creates a relationship between two tables.
    
    A FOREIGN KEY is a field (or collection of fields) in one table, that refers to the PRIMARY KEY in another table.


## What is the Difference between Primary Key and Unique Key
- UNIQUE KEY allows NULL values
- PRIMARY KEY does not allow NULL values.
- There is only One Primary Key per Table but you can have Multiple Unique Keys per Table.



## INDEX
- Indexes are used to retrieve data from the database more quickly than otherwise. The users cannot see the indexes, they are just used to speed up searches/queries.

> Note: Updating a table with indexes takes more time than updating a table without (because the indexes also need an update). So, only create indexes on columns that will be frequently searched against.

```sql
CREATE INDEX index_name
ON table_name (column1, column2, ...);

CREATE UNIQUE INDEX index_name
ON table_name (column1, column2, ...);

CREATE INDEX idx_lastname
ON Persons (LastName);

CREATE INDEX idx_pname
ON Persons (LastName, FirstName);

ALTER TABLE table_name
DROP INDEX index_name;
```




```sql
CREATE DATABASE EmployeeDetails;

USE EmployeeDetails;

SHOW TABLES;

CREATE TABLE employees(
empId INT AUTO_INCREMENT PRIMARY KEY,
empName VARCHAR(255) NOT NULL,
empSalary DECIMAL(10,2) NOT NULL );

DESC employees;

INSERT INTO employees(empName,empSalary) VALUES('John Doe', 50000.00);
INSERT INTO employees(empName,empSalary) VALUES('Jane Smith', 60000.00);
INSERT INTO employees(empName,empSalary) VALUES('Alice Johnson', 55000.00);
INSERT INTO employees(empName,empSalary) VALUES('Bob Brown', 70000.00);
INSERT INTO employees(empName,empSalary) VALUES('Charlie Davis', 45000.00);


SELECT * FROM employees;

ALTER TABLE employees ADD empAge int;

```

## To fetch only the first 10 records from a MySQL database, you can use the `LIMIT` clause in your SQL query.
    Here's an example query:
```sql
SELECT * FROM your_table_name LIMIT 10;
```
## To retrieve the last 10 records from a MySQL database, you can combine the `ORDER BY` and `LIMIT` clauses in your SQL query.
    Here's an example query:
```sql
SELECT * FROM your_table_name ORDER BY id DESC LIMIT 10;
```


```
https://www.sql-practice.com/
SELECT * FROM patients

-- Show the city and the total number of patients in the city.
--Order from most to least patients and then by city name ascending.

select city ,count(patient_id) as TOTAL_NUMBER FROM patients group by CITY order by TOTAL_NUMBER ;
```