# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
Create a table named Locations with the following columns:

*LocationID as INTEGER

*LocationName as TEXT

*Address as TEXT

```sql
create TABLE Locations(
LocationID INTEGER,
LocationName TEXT,
Address TEXT
);
```

**Output:**

<img width="1286" height="240" alt="image" src="https://github.com/user-attachments/assets/284b89e6-0b90-4f1f-a7f0-828d6283a65b" />

**Question 2**
---
Create a table named Invoices with the following constraints:

*InvoiceID as INTEGER should be the primary key.

*InvoiceDate as DATE.

*DueDate as DATE should be greater than the InvoiceDate.

*Amount as REAL should be greater than 0.

```sql
create table Invoices(
InvoiceID INTEGER PRIMARY KEY,
InvoiceDate DATE,
DueDate DATE check(Duedate>InvoiceDate),
Amount REAL check(Amount>0)
);
```

**Output:**

<img width="1002" height="161" alt="image" src="https://github.com/user-attachments/assets/364cf29f-543b-48aa-93af-44e50e70a07d" />

**Question 3**
---
Create a table named Products with the following constraints:

*ProductID as INTEGER should be the primary key.

*ProductName as TEXT should be unique and not NULL.

*Price as REAL should be greater than 0.

*StockQuantity as INTEGER should be non-negative.

```sql
-create TABLE Products(
ProductID INTEGER PRIMARY KEY,
ProductName TEXT UNIQUE NOT NULL,
Price REAL check(Price>0),
StockQuantity INTEGER check(StockQuantity>0)
);
```

**Output:**

<img width="1144" height="101" alt="image" src="https://github.com/user-attachments/assets/00ec278e-6e78-4f95-ba82-986f3a46bbfa" />


**Question 4**
---
Insert the following employees into the Employee table:

EmployeeID  Name        Position    Department  Salary

2           John Smith  Developer   IT          75000

3           Anna Bell   Designer    Marketing   68000

```sql
insert into Employee
values(2,'John Smith','Developer',  'IT',   75000),
(3  , 'Anna Bell', 'Designer', 'Marketing', 68000);
```

**Output:**

<img width="1219" height="177" alt="image" src="https://github.com/user-attachments/assets/c04f5060-aef4-4acd-beac-7994a4203696" />


**Question 5**
---
Write a SQL query to add a new column MobileNumber of type NUMBER and a new column Address of type VARCHAR(100) to the Student_details table.

```sql
-alter table Student_details
ADD COLUMN MobileNumber NUMBER;
ALTER TABLE Student_details
ADD COLUMN Address VARCHAR(100);
```

**Output:**

<img width="1169" height="193" alt="image" src="https://github.com/user-attachments/assets/c3a92f17-3d2d-4c44-ab79-4c9d68253f08" />

**Question 6**
---
Create a new table named item with the following specifications and constraints:

*item_id as TEXT and as primary key.

*item_desc as TEXT.

*rate as INTEGER.

*icom_id as TEXT with a length of 4.

*icom_id is a foreign key referencing com_id in the company table.

*The foreign key should cascade updates and deletes.

*item_desc and rate should not accept NULL.

```sql
create table item
(
item_id TEXT PRIMARY KEY,
item_desc TEXT NOT NULL,
rate INTEGER NOT NULL,
icom_id char(4),
FOREIGN KEY(icom_id) references company(com_id)
ON UPDATE cascade
ON DELETE cascade
);
```

**Output:**

<img width="1046" height="178" alt="image" src="https://github.com/user-attachments/assets/9a5a2153-8d91-4215-a833-5cfccf3865c8" />


**Question 7**
---
Insert all customers from Old_customers into Customers

Table attributes are CustomerID, Name, Address, Email

```sql
insert into Customers(CustomerID,Name,Address,Email)
select CustomerID,Name,Address,Email from Old_customers;
```

**Output:**

<img width="1074" height="149" alt="image" src="https://github.com/user-attachments/assets/3609c3a9-ae5a-4191-bae1-a7c1d67193bf" />


**Question 8**
---
Write a SQL query for adding a new column named "email" with the datatype VARCHAR(100) to the  table "customer" 

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 

        3002 | Nick Rimando   | New York   |   100 |        5001
        
        3007 | Brad Davis     | New York   |   200 |        5001
        
        3005 | Graham Zusi    | California |   200 |        5002

```sql
ALTER TABLE customer
add column email VARCHAR(100);
```

**Output:**

<img width="1300" height="220" alt="image" src="https://github.com/user-attachments/assets/ae4e5305-5cb5-4daa-bca2-581f20cf637a" />


**Question 9**
---
Insert the below data into the Books table, allowing the Publisher and Year columns to take their default values.

ISBN             Title                 Author


978-6655443321   Big Data Analytics    Karen Adams

Note: The Publisher and Year columns will use their default values.

```sql
INSERT INTO Books (ISBN,Title,Author)
VALUES ('978-6655443321','Big Data Analytics', 'Karen Adams');
```

**Output:**

<img width="931" height="192" alt="image" src="https://github.com/user-attachments/assets/0a2d5dab-d4d1-48c3-8c34-7baf2a42098e" />

**Question 10**
---
Create a table named Invoices with the following constraints:

*InvoiceID as INTEGER should be the primary key.

*InvoiceDate as DATE.

*Amount as REAL should be greater than 0.

*DueDate as DATE should be greater than the InvoiceDate.

*OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```sql
create table Invoices(
InvoiceID INTEGER PRIMARY KEY,
InvoiceDate DATE,
Amount REAL check(Amount>0),
DueDate check(DueDate>INvoicedate),
OrderID INTEGER,
FOREIGN KEY(OrderID) references Orders(OrderID)
)
```

**Output:**

<img width="1298" height="186" alt="image" src="https://github.com/user-attachments/assets/03be7394-2af3-4e65-b303-bb34144bcfc3" />

## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
