
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