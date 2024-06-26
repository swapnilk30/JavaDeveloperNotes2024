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

```