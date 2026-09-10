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
Write a SQL Query to find how many medications are prescribed for each patient?

Sample table:MedicalRecords Table
```sql
select PatientID , count(Medications) as AvgMedications 
from MedicalRecords 
group by PatientID ;
```

**Output:**

<img width="996" height="560" alt="image" src="https://github.com/user-attachments/assets/ce70fdc3-de1d-44a1-93f5-6ea8c6a5601b" />


**Question 2**
---
What is the count of male and female patients?

Sample table: Patients Table
```sql
select Gender , count(*) as TotalPatients 
from Patients
group by Gender;
```

**Output:**

<img width="999" height="363" alt="image" src="https://github.com/user-attachments/assets/7f1c7b9c-fb0d-4390-b101-3e8f3519daff" />


**Question 3**
---
How many medical records are there for each patient?

Sample table:MedicalRecords Table


```sql
select PatientID, count(*) as  TotalRecords 
from MedicalRecords
group by PatientID;
```

**Output:**

<img width="881" height="588" alt="image" src="https://github.com/user-attachments/assets/182a27ff-ce4b-459e-bf87-6fe541554bd3" />


**Question 4**
---
Write a SQL query to find the average length of email addresses (in characters):

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT
city        TEXT
email       TEXT
phone       INTEGER

```sql
select avg(length(email)) as avg_email_length 
from customer;

```

**Output:**

<img width="772" height="330" alt="image" src="https://github.com/user-attachments/assets/1d151918-356b-4dc6-a1f2-b907040e6d83" />


**Question 5**
---
Write a SQL query to find the total amount of fruits with a unit type of 'LB'.

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
select sum(inventory) as total
from fruits
where unit = 'LB';
```

**Output:**

<img width="931" height="369" alt="image" src="https://github.com/user-attachments/assets/8a8916c3-c0e8-4210-b8f5-1edd8976d67b" />

**Question 6**
---
Write a SQL query to Calculate the average income of the employees with names starting with 'A': 

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER

```sql
select avg(income) as avg_income 
from employee
where name like 'A%';
```

**Output:**

<img width="848" height="333" alt="image" src="https://github.com/user-attachments/assets/1376ec9b-e0d2-41f7-99a2-bdc97c26c499" />


**Question 7**
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
select name as Employee_Name , age as Age
from employee
order by age asc limit 1;
```

**Output:**

<img width="948" height="331" alt="image" src="https://github.com/user-attachments/assets/8684a354-dff2-44f8-b4a3-2071c4934318" />


**Question 8**
---
Write the SQL query that accomplishes the grouping of data by age intervals using the expression (age/5)5, calculates the minimum age for each group, and excludes groups where the minimum age is not less than 25.

Sample table: customer1

```sql
select (age/5)*5 as age_group , MIN(age)
from customer1
group by  (age/5) *5 
having MIN(age) <25;
```

**Output:**

<img width="938" height="330" alt="image" src="https://github.com/user-attachments/assets/88fed5aa-191f-4df2-a0a7-19775eb92cea" />


**Question 9**
---
Write the SQL query that accomplishes the grouping of data by age, calculates the total income for each age group, and includes only those age groups where the total income sum is greater than 1,000,000.

Sample table: employee

```sql
select age , SUM(income)
from employee
group by age
having sum(income) > 1000000;
```

**Output:**

<img width="951" height="434" alt="image" src="https://github.com/user-attachments/assets/7b9a8973-6ade-4e89-86e9-54555498a61a" />

**Question 10**
---
Write the SQL query that accomplishes the selection of total number of products for each category from the "products" table, and includes only those products where the minimum category ID is less than 3.

Sample table: products

```sql
select category_id, count(product_name)
from products
group by category_id 
having category_id < 3;
```

**Output:**
<img width="945" height="359" alt="image" src="https://github.com/user-attachments/assets/ee772be5-e3ed-4b4e-87fd-417f98a24051" />




## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
