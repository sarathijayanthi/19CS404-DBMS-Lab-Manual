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
<img width="778" height="482" alt="image" src="https://github.com/user-attachments/assets/f61ffacb-5676-40ca-aacf-cf1dd65ef996" />


```sql
create table item(
item_id text primary key,
item_desc text not null,
rate integer not null,
icom_id text check (length(icom_id)=4),
foreign key (icom_id) references company(com_id) on update cascade on delete cascade

);
```

**Output:**

<img width="648" height="332" alt="image" src="https://github.com/user-attachments/assets/40f8a94e-f8ec-445a-97e0-3f707d8f01ee" />

**Question 2**
---
<img width="785" height="416" alt="image" src="https://github.com/user-attachments/assets/7b44da18-93ed-46dc-b048-fb410de728e1" />

```sql
insert into Student_details
select RollNo, Name, Gender, Subject, MARKS
from Archived_students;
```

**Output:**

<img width="630" height="243" alt="image" src="https://github.com/user-attachments/assets/c9a81470-f36a-4053-86b0-cd31abb567f0" />


**Question 3**
---
<img width="773" height="398" alt="image" src="https://github.com/user-attachments/assets/ea6dce92-5173-4726-9670-7ee1144be089" />


```sql
ALTER TABLE Employees
ADD salary INTEGER CHECK (salary > 0);
```

**Output:**

<img width="700" height="291" alt="image" src="https://github.com/user-attachments/assets/557857c5-ba65-4b24-b792-7a8ae51bb27f" />


**Question 4**
---
<img width="857" height="345" alt="image" src="https://github.com/user-attachments/assets/bfae251d-0050-4a03-bd62-ce7ee230f4a6" />


```sql
INSERT INTO Employee
values(001, 'Sarah Parker', 'Manager', 'HR',60000);
```

**Output:**

<img width="715" height="205" alt="image" src="https://github.com/user-attachments/assets/fe0edf7a-300a-4fe8-94aa-157ad770764a" />


**Question 5**
---
<img width="836" height="431" alt="image" src="https://github.com/user-attachments/assets/cad9e2b2-1138-494e-bd3b-4cd995644764" />


```sql
create table Orders(
OrderID INTEGER,
OrderDate TEXT,
CustomerID INTEGER
```

**Output:**

<img width="695" height="369" alt="image" src="https://github.com/user-attachments/assets/9f8f43fb-3e27-4626-87cc-8207e54a6d4c" />


**Question 6**
---
<img width="811" height="450" alt="image" src="https://github.com/user-attachments/assets/ced82898-9955-44d1-b211-a8b247c0f9c9" />

```sql
create table jobs(
job_id INTEGER,
job_title TEXT DEFAULT NULL,
min_salary INTEGER DEFAULT 8000,
max_salary INTEGER max NULL

);
```

**Output:**

<img width="684" height="349" alt="image" src="https://github.com/user-attachments/assets/b46a6053-a0fc-4f99-a66c-1db09a57183d" />


**Question 7**
---

<img width="796" height="450" alt="image" src="https://github.com/user-attachments/assets/e139f77f-7370-4118-94ea-540f7d032036" />


```sql
create table Attendance(
AttendanceID INTEGER PRIMARY KEY,
EmployeeID INTEGER REFERENCES Employees(EmployeeID),
AttendanceDate DATE not null,
Status TEXT CHECK (Status in ('present', 'Absent', 'Leave'))
);
```

**Output:**

<img width="601" height="260" alt="image" src="https://github.com/user-attachments/assets/f8444858-c9af-4364-99d7-66e1c057c27f" />


**Question 8**
---
<img width="702" height="381" alt="image" src="https://github.com/user-attachments/assets/f84f4966-8433-4ddb-a92e-d640ca63f614" />


```sql
create table Shipments(
ShipmentID INTEGER PRIMARY KEY,
ShipmentDate DATE,
SupplierID INTEGER REFERENCES Suppliers(SupplierID),
OrderID INTEGER REFERENCES Orders(OrderID)

);
```

**Output:**

<img width="710" height="218" alt="image" src="https://github.com/user-attachments/assets/b27e07e2-3afb-4887-a822-c9c2ab603101" />

**Question 9**
---
<img width="789" height="485" alt="image" src="https://github.com/user-attachments/assets/91936979-0b89-408f-b035-1c16161eeaad" />


```sql

insert into Employee
values
'George Clark',
, 'Noah Davis'
'Ava Miller',

(5,
(7
(8,

'Manager',

'Consultant', null, null),
'HR' ,60000),
'Consultant', 'IT',null);
```

**Output:**

<img width="665" height="237" alt="image" src="https://github.com/user-attachments/assets/f76f8ab7-0607-4088-91bd-431dbe423c38" />


**Question 10**
---
<img width="770" height="294" alt="image" src="https://github.com/user-attachments/assets/0cd22885-2803-453c-ac2e-4d11dda8dc18" />

```sql
alter table employee add designation varchar(50);
```

**Output:**

<img width="706" height="279" alt="image" src="https://github.com/user-attachments/assets/b05132b8-57cf-433c-bb72-53419b8b8ac7" />

##GRADE:##
<img width="500" height="218" alt="image" src="https://github.com/user-attachments/assets/11e0e0b5-6369-43c6-932d-f89da84f0e7a" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
