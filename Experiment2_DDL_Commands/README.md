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
---
Create a table named Employees with the following constraints:

EmployeeID should be the primary key.
FirstName and LastName should be NOT NULL.
Email should be unique.
Salary should be greater than 0.
DepartmentID should be a foreign key referencing the Departments table.

```sql
 create table Employees (
    EmployeeID integer primary key,
    FirstName varchar[100] not null,
    LastName varchar[100] not null ,
    Email varchar[100] UNIQUE ,
    Salary int check(salary > 0),
    DepartmentID int,
    foreign key(departmentid) references departments(departmentid));
```

**Output:**

<img width="1268" height="464" alt="image" src="https://github.com/user-attachments/assets/131a1109-6269-495e-b7a8-f2ed36b57705" />


**Question 2**
---
 Insert the below data into the Student_details table, allowing the Subject and MARKS columns to take their default values.

RollNo      Name          Gender      
----------  ------------  ----------  
204         Samuel Black  M          

Note: The Subject and MARKS columns will use their default values.

```sql
insert into Student_Details(Rollno,Name,Gender) values(204,"Samuel Black","M");
```

**Output:**

<img width="1267" height="358" alt="image" src="https://github.com/user-attachments/assets/47d83820-e00e-4437-a15d-c4916cd2eaed" />


**Question 3**
---
Create a table named Locations with the following columns:

LocationID as INTEGER
LocationName as TEXT
Address as TEXT

```sql
create table locations(
LocationID INTEGER,
LocationName TEXT,
Address TEXT);
```

**Output:**

<img width="1261" height="420" alt="image" src="https://github.com/user-attachments/assets/9e80f574-aec4-42ed-8846-622754b71eac" />


**Question 4**
---
create a table named jobs including columns job_id, job_title, min_salary and max_salary, and make sure that, the default value for job_title is blank and min_salary is 8000 and max_salary is NULL will be entered automatically at the time of insertion if no value assigned for the specified columns.

```sql
create table jobs(job_id INTEGER,
        job_title TEXT,
        min_salary INTEGER default 8000,
        max_salary INTEGER default null
);
```

**Output:**

<img width="1265" height="380" alt="image" src="https://github.com/user-attachments/assets/84efc753-344f-4367-9386-fb7af490b694" />


**Question 5**
---
Create a table named Attendance with the following constraints:
AttendanceID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
AttendanceDate as DATE.
Status as TEXT should be one of 'Present', 'Absent', 'Leave'.

```sql
create table Attendance (
    AttendanceID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
      AttendanceDate DATE,
      Status TEXT CHECK(Status IN('Present','Absent','Leave')),
    FOREIGN KEY(EmployeeID) REFERENCES Employees(EmployeeID)
);
```

**Output:**

<img width="1266" height="344" alt="image" src="https://github.com/user-attachments/assets/19ca441a-862c-4763-9107-9ddd05902675" />


**Question 6**
---
Write a SQL Query  to change the name of attribute "name" to "first_name"  and add mobilenumber as number ,DOB as Date in the table Companies. 

```sql
ALTER TABLE Companies Rename column name to first_name;
alter table companies add column mobilenumb number;
alter table companies add column DOB Date;
```

**Output:**

<img width="1265" height="432" alt="image" src="https://github.com/user-attachments/assets/006429c8-98e8-4f64-be19-90b72af328eb" />


**Question 7**
---
Insert all books from Out_of_print_books into Books

Table attributes are ISBN, Title, Author, Publisher, YearPublished

```sql
insert into books select * from Out_of_print_books;
```

**Output:**

<img width="1266" height="341" alt="image" src="https://github.com/user-attachments/assets/ea9e7040-5fd9-4c10-8964-ac3044f05deb" />


**Question 8**
---
Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```sql
create table Invoices (
    InvoiceID INTEGER  PRIMARY KEY,
    InvoiceDate DATE,
    Amount REAL CHECK(Amount>0),
    DueDate DATE CHECK(DueDate>InvoiceDate),
    OrderID INTEGER,
    FOREIGN KEY(OrderID) References Orders(OrderID));
```

**Output:**

<img width="1260" height="338" alt="image" src="https://github.com/user-attachments/assets/7f330fa3-25f9-433f-a412-ff84cfb1c26c" />


**Question 9**
---
Write an SQL command can to add a column named email of type TEXT to the customers table

```sql
alter table customers add email TEXT;

```

**Output:**
<img width="1265" height="340" alt="image" src="https://github.com/user-attachments/assets/ea7c9a41-7116-4061-a0d7-0d13b8221975" />




**Question 10**
---
Insert the following students into the Student_details table:
RollNo      Name        Gender      Subject     MARKS
----------  ----------  ----------  ----------  ----------
202            Ella King         F           Chemistry   87
203            James Bond   M          Literature    78

```sql
insert into Student_details(RollNo,Name,Gender,Subject,MARKS) values(202,'Ella King','F','Chemistry',87),(203,'James Bond','M','Literature',78);
```

**Output:**

<img width="1266" height="320" alt="image" src="https://github.com/user-attachments/assets/557dcb7e-ee47-4a8f-859d-e2c9d3442b3c" />

**Module SEB:**
<img width="1100" height="73" alt="image" src="https://github.com/user-attachments/assets/d3498252-2089-48be-9cc3-05a24e8c1357" />
<img width="1121" height="72" alt="image" src="https://github.com/user-attachments/assets/c0e08301-7d01-41ba-9013-e821e32e99ab" />


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
