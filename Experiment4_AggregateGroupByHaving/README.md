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
How many male and female doctors are there in each medical specialty?

Sample table:Doctors Table

```sql
select specialty, gender, count(doctorID) AS TotalDoctors from Doctors Group by Specialty , Gender order by Specialty , gender ;
```

**Output:**

<img width="1257" height="665" alt="image" src="https://github.com/user-attachments/assets/25088f41-15c2-4414-9f09-53d99710fd3d" />


**Question 2**
---
How many medical records were created in each month?
Sample table:MedicalRecords Table

```sql
select strftime('%Y-%m',Date) as Month,
count(*) as TotalRecords 
from medicalrecords 
group by strftime('%Y-%m',date)
order by Month;
```

**Output:**

<img width="1264" height="468" alt="image" src="https://github.com/user-attachments/assets/fe006ae9-774e-4c92-9a6a-af3c27cd0ded" />


**Question 3**
---
What is the most common diagnosis among patients?
Sample table:MedicalRecords Table

```sql
select Diagnosis , count(*) as DiagnosisCount
from medicalrecords
group by Diagnosis
order by DiagnosisCount desc
limit 1;
```

**Output:**

<img width="1264" height="349" alt="image" src="https://github.com/user-attachments/assets/53027b85-a210-4734-b0d4-c587665a4f81" />


**Question 4**
---
Write a SQL query that counts the number of unique salespeople. Return number of salespeople.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

```sql
select count(distinct salesman_id) as COUNT from orders ;
```

**Output:**

<img width="1259" height="361" alt="image" src="https://github.com/user-attachments/assets/11c3a5ff-db43-48d8-87cf-d089b0b88d39" />


**Question 5**
---
Write a SQL query to calculate total purchase amount of all orders. Return total purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

```sql
select SUM(purch_amt) as TOTAL from orders ;
```

**Output:**
<img width="1257" height="355" alt="Screenshot 2025-10-23 050627" src="https://github.com/user-attachments/assets/b80ee37b-3b19-4915-99b7-8f620a1be6d4" />



**Question 6**
---
Write a SQL query to find the Fruit with the lowest available quantity.

Note: Inventory attribute contains amount of fruits

Table: fruits

name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL

```sql
select name as fruit_name , inventory as lowest_quantity from fruits where inventory = (select min(inventory) from fruits) ;
```

**Output:**

<img width="1263" height="359" alt="image" src="https://github.com/user-attachments/assets/cbd20ef7-3abe-4b32-87be-294024771a0a" />


**Question 7**
---
Write a SQL query to find the total income of employees aged 40 or above.

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER

```sql
select sum(income) as total_income from employee where age >=40;
```

**Output:**

<img width="1253" height="355" alt="image" src="https://github.com/user-attachments/assets/f8a2dbb0-b047-4a8a-a679-d189fd4de109" />


**Question 8**
---
Write the SQL query that accomplishes the selection of product which has lowest price in each category from the "products" table and includes only those products where the minimum price is less than 10.

Sample table: products

```sql
select category_id , min(price) as Price from products group by category_id having min(price) < 10 ;
```

**Output:**

<img width="1258" height="394" alt="image" src="https://github.com/user-attachments/assets/1e3edb3d-53b2-4224-b1ed-64d5d4ec8dc8" />


**Question 9**
---
Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the average work hours for each date, and excludes dates where the average work hour is not less than 10.

Sample table: employee1

```sql
select jdate , AVG(workhour) from employee1 group by jdate having avg(workhour) < 10 ;
```

**Output:**

<img width="1264" height="379" alt="image" src="https://github.com/user-attachments/assets/35158496-93d3-42a0-9e46-3b680a3da5cd" />


**Question 10**
---
Write a SQL query to identify the cities (addresses) where the average salary is greater than Rs. 5000, as per the "customer1" table.

Sample table: customer1

```sql
select address , AVG(salary) from customer1 group by address having AVG(salary) > 5000;
```

**Output:**

<img width="1250" height="467" alt="image" src="https://github.com/user-attachments/assets/225bcfb6-5995-4646-b8b4-1b9976d16b1e" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
