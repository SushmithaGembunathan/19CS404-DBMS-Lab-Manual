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
Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 1 million

Employee Table

name             type

------------   ---------------

id                    INTEGER

name              TEXT

age                 INTEGER

city                 TEXT

income           INTEGER

```sql
SELECT
    id,
    name,
    age,
    city,
    income
FROM
    Employee
WHERE
    age < (SELECT AVG(age) FROM Employee WHERE income > 1000000);
```

**Output:**

<img width="1308" height="439" alt="image" src="https://github.com/user-attachments/assets/2eefec85-0fa4-44a1-a885-dbd08a81a0b6" />


**Question 2**
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
SELECT *
FROM CUSTOMERS
WHERE SALARY = 1500;
```

**Output:**

<img width="1306" height="381" alt="image" src="https://github.com/user-attachments/assets/5a3340db-2fba-4f6b-92dd-ac7a9bb2eb43" />


**Question 3**
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
SELECT *
FROM CUSTOMERS
WHERE SALARY > 1500;
```

**Output:**
<img width="1312" height="629" alt="Screenshot 2025-10-30 113417" src="https://github.com/user-attachments/assets/4acb592b-3476-4b6b-a425-f470b1f7fc9e" />



**Question 4**
---
Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)

```sql
SELECT
    g1.student_name,
    g1.grade
FROM
    GRADES g1
INNER JOIN (
    SELECT
        subject,
        MAX(grade) AS max_grade
    FROM
        GRADES
    GROUP BY
        subject
) g2 ON g1.subject = g2.subject AND g1.grade = g2.max_grade;
```

**Output:**

<img width="1311" height="467" alt="image" src="https://github.com/user-attachments/assets/1d6c6d96-d1b3-4be9-863a-f16e335beb0c" />


**Question 5**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is LESS than $2500.

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
SELECT *
FROM CUSTOMERS
WHERE SALARY < 2500;
```

**Output:**

<img width="1311" height="498" alt="image" src="https://github.com/user-attachments/assets/c22cb21c-1a20-4a5c-a32f-1808f9e4e690" />


**Question 6**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $4500.

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
SELECT *
FROM CUSTOMERS
WHERE SALARY > 4500;
```

**Output:**

<img width="1316" height="459" alt="image" src="https://github.com/user-attachments/assets/4058bed9-1c59-40df-a274-157f4409394e" />


**Question 7**
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
-- SELECT name, city
FROM customer
WHERE city IN (SELECT city FROM customer WHERE id IN (3, 7));
```

**Output:**

<img width="980" height="487" alt="image" src="https://github.com/user-attachments/assets/9f00aeb3-5f07-4d6e-a3e9-f36f32aa0c1d" />


**Question 8**
---
Write a SQL query that retrieve all the columns from the table "Grades", where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)



```sql
-- SELECT
    student_id,
    student_name,
    subject,
    grade
FROM
    Grades g1
WHERE
    grade = (
        SELECT
            MAX(grade)
        FROM
            Grades g2
        WHERE
            g1.subject = g2.subject
    );
```

**Output:**

<img width="1302" height="460" alt="image" src="https://github.com/user-attachments/assets/b320ef8b-e5ea-4bdb-af14-9fcd13086ed2" />


**Question 9**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi

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
SELECT *
FROM CUSTOMERS
WHERE ADDRESS = 'Delhi';
```

**Output:**

<img width="1307" height="376" alt="image" src="https://github.com/user-attachments/assets/cbb15374-8f95-43d0-8703-0e5fcc5e167c" />


**Question 10**
---
 Write a SQL query to Retrieve the names of customers who have a phone number that is not shared with any other customer.

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER

```sql
-- SELECT name
FROM customer
WHERE phone IN (
    SELECT phone
    FROM customer
    GROUP BY phone
    HAVING COUNT(phone) = 1
);
```

**Output:**

<img width="1311" height="490" alt="image" src="https://github.com/user-attachments/assets/2d7fd1ee-ac1f-4b44-9099-7b6996f9fc34" />



## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
