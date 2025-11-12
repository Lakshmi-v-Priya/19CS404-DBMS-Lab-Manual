# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
How many doctors specialize in each medical specialty?

Sample table:Doctors Table

```sql
select Specialty,count(Specialty)as TotalDocto from Doctors
group by Specialty;
```

**Output:**

<img width="668" height="656" alt="image" src="https://github.com/user-attachments/assets/3aa4d40f-ce32-4749-84cf-822215f024cd" />

**Question 2**
---
What is the total number of appointments scheduled by each doctor?

Sample table:Appointments Table

```sql
select DoctorID,count(*)as TotalAppointments from Appointments
group by DoctorID;
```

**Output:**

<img width="659" height="595" alt="image" src="https://github.com/user-attachments/assets/74a4af68-ad2e-4ee7-b810-5b77b997ca6a" />

**Question 3**
---
How many medical records were created in each month?

Sample table:MedicalRecords Table

```sql
SELECT STRFTIME('%Y-%m',Date) AS Month,
COUNT(*) AS TotalRecords
FROM MedicalRecords
group by Month
Order BY Month;
```

**Output:**

<img width="577" height="407" alt="image" src="https://github.com/user-attachments/assets/14b06293-8034-43f8-9873-fd27d6d77c8a" />

**Question 4**
---
Write a SQL query to calculate total purchase amount of all orders. Return total purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

```sql
select SUM(purch_amt)as TOTAL FROM orders;
```

**Output:**

<img width="335" height="280" alt="image" src="https://github.com/user-attachments/assets/69abc6ff-100f-4b57-b3c9-91d82f9f8efb" />

**Question 5**
---
Write a SQL query to find the number of employees who are having the same age removing the duplicate values.

Sample table: employee

```sql
select COUNT(DISTINCT age)AS COUNT
FROM employee;
```

**Output:**

<img width="319" height="237" alt="image" src="https://github.com/user-attachments/assets/eae5815b-76e3-4081-87ed-61018b8e9b34" />

**Question 6**
---
Write a SQL query to find the youngest employee in the company?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER

```sql
SELECT name as Employee_Name,age as Age FROM employee
ORDER by age ASC
LIMIT 1;
```

**Output:**

<img width="591" height="242" alt="image" src="https://github.com/user-attachments/assets/e55c1919-fde7-4ce1-98a8-42b9e76ecc47" />

**Question 7**
---
Write a SQL query to determine the number of customers who received at least one grade for their activity.

Sample table: customer

customer_id |   cust_name    |    city    | grade | salesman_id 

-------------+----------------+------------+-------+-------------

        3002 | Nick Rimando   | New York   |   100 |        5001

        3007 | Brad Davis     | New York   |   200 |        5001

        3005 | Graham Zusi    | California |   200 |        5002

```sql
select count(cust_name)as COUNT FROM customer
where grade is NOT NULL;
```

**Output:**

<img width="336" height="238" alt="image" src="https://github.com/user-attachments/assets/0e8a1e47-a702-4bec-b35d-49753a4dc7a9" />

**Question 8**
---
Write the SQL query that achieves the grouping of data by city, calculates the total income for each city, and includes only those cities where the total income sum is greater than 200,000.

Sample table: employee

```sql
select city,Sum(Income)as Income
from employee
group by city
having Sum(Income)>200000;
```

**Output:**

<img width="539" height="465" alt="image" src="https://github.com/user-attachments/assets/4122d049-16a1-4ec9-9582-0a198bb91e19" />

**Question 9**
---
Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the minimum work hours for each date, and excludes dates where the minimum work hour is not less than 10.

Sample table: employee1

```sql
SELECT jdate ,MIN(workhour)
from employee1
group by jdate
having MIN(workhour)<10;
```

**Output:**

<img width="596" height="361" alt="image" src="https://github.com/user-attachments/assets/bfcc37f4-7993-46b8-8c56-58de643d00f4" />

**Question 10**
---
Write the SQL query to find how many patients have more than 3 medical records?.

Sample table: MedicalRecords

name        type
----------  ----------
RecordID    INTEGER
PatientID   INTEGER
DoctorID    INTEGER
Date        DATE
Diagnosis   TEXT
Treatment   TEXT
Medication  TEXT

```sql
select PatientID,COUNT(*)AS TotalRecords
from MedicalRecords
group by PatientID
HAVING COUNT(*)>3;
```

**Output:**
<img width="581" height="266" alt="image" src="https://github.com/user-attachments/assets/aab18a6d-ed83-41eb-9433-96ebd80efd30" />

## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
