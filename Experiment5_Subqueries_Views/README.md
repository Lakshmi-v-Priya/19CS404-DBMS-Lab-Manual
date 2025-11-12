# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
Write a SQL query to Retrieve the medications with dosages equal to the highest dosage

Table Name: Medications (attributes: medication_id, medication_name, dosage)

```sql
SELECT * FROM  Medications
WHERE dosage IN (SELECT MAX(dosage) FROM Medications);
```

**Output:**

<img width="848" height="334" alt="image" src="https://github.com/user-attachments/assets/752f21e2-b74d-4ddd-b43b-db2106f9076b" />

**Question 2**
---
From the following tables, write a SQL query to find those salespeople who earned the maximum commission. Return ord_no, purch_amt, ord_date, and salesman_id.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

orders table

name             type
---------------  --------
order_no         int
purch_amt        real
order_date       text
customer_id      int
salesman_id      int

```sql
SELECT ord_no,purch_amt,ord_date,salesman_id FROM orders
WHERE salesman_id IN(SELECT salesman_id FROM salesman
WHERE commission=(SELECT MAX(commission) FROM salesman));
```

**Output:**

<img width="994" height="403" alt="image" src="https://github.com/user-attachments/assets/d20a1781-1f2d-4ea5-92be-3bfc8ab19554" />

**Question 3**
---
Write a SQL query to List departments with names longer than the average length

Departments Table (attributes: department_id, department_name)

```sql
SELECT * FROM Departments
WHERE LENGTH(department_name)>(SELECT AVG(LENGTH(department_name)) FROM Departments);
```

**Output:**

<img width="534" height="324" alt="image" src="https://github.com/user-attachments/assets/c422b6dc-4813-48d3-bd96-ddd125caa156" />

**Question 4**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose AGE is LESS than $30

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

```sql
SELECT * FROM CUSTOMERS
WHERE AGE<30;
```

**Output:**

<img width="1183" height="513" alt="image" src="https://github.com/user-attachments/assets/d3b1fce0-398b-4cbb-a615-c66b5ee1c6c3" />

**Question 5**
---
Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 2.5 Lakh

Employee Table

name             type

------------   ---------------

id                    INTEGER

name              TEXT

age                 INTEGER

city                 TEXT

income           INTEGER

```sql
SELECT * FROM Employee
WHERE age<(SELECT AVG(age) FROM Employee WHERE income >250000);
```

**Output:**

<img width="1235" height="470" alt="image" src="https://github.com/user-attachments/assets/97f9dcb7-f143-4825-8752-3561136f4a0d" />

**Question 6**
---
Write a SQL query to Retrieve the names and cities of customers who have the same city as customers with IDs 3 and 7

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER

```sql
SELECT name,city FROM customer
WHERE city IN(SELECT city FROM customer WHERE id IN(3,7));
```

**Output:**

<img width="532" height="380" alt="image" src="https://github.com/user-attachments/assets/6dd60f49-a628-4eaa-97bd-8ff20f8d35db" />


**Question 7**
---
Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the minimum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)

```sql
SELECT student_name, grade FROM GRADES g
WHERE grade=(SELECT MIN(grade) FROM GRADES 
        WHERE subject=g.subject);
```

**Output:**

<img width="717" height="358" alt="image" src="https://github.com/user-attachments/assets/3b4c8a42-b1c1-45e5-90ed-4a373ce61aba" />

**Question 8**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is EQUAL TO $1500.

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

```sql
SELECT * FROM CUSTOMERS
WHERE SALARY = 1500;
```

**Output:**

<img width="1188" height="267" alt="image" src="https://github.com/user-attachments/assets/17b019c4-2cd0-43a4-9128-0a25dcb0f1ab" />

**Question 9**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $1500.

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

```sql
SELECT * FROM CUSTOMERS
WHERE SALARY > 1500;
```

**Output:**

<img width="1187" height="536" alt="image" src="https://github.com/user-attachments/assets/5bab2bea-de1e-4825-865f-8d13a1aa23e8" />

**Question 10**
---
From the following tables, write a SQL query to find all the orders generated in New York city. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.

SALESMAN TABLE

name               type
-----------        ----------
salesman_id  numeric(5)
name             varchar(30)
city                 varchar(15)
commission   decimal(5,2)

ORDERS TABLE

name            type
----------      ----------
ord_no          int
purch_amt    real
ord_date       text
customer_id  int
salesman_id  int

```sql
SELECT * FROM ORDERS
WHERE salesman_id IN( SELECT salesman_id FROM SALESMAN WHERE city="New York");
```

**Output:**

<img width="1226" height="412" alt="image" src="https://github.com/user-attachments/assets/e7308fa0-4d51-40fa-9814-413406e18569" />

## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
