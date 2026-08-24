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
<img width="1433" height="575" alt="image" src="https://github.com/user-attachments/assets/120ad7ba-0368-470b-a21e-13ae0d3d09c1" />


```sql
select frequency,count(*) as
TotalPrescriptions from Prescriptions
group by frequency;

```

**Output:**
<img width="1433" height="551" alt="image" src="https://github.com/user-attachments/assets/58def58f-b19b-4596-8e5d-1999b0f12d36" />


**Question 2**
---
<img width="1433" height="553" alt="image" src="https://github.com/user-attachments/assets/451de0b0-5b3a-45d2-823e-1e975ab0fcc6" />


```sql
select DoctorID,count(AppointmentID) as TotalAppointments
from Appointments
group by DoctorID;
```

**Output:**
<img width="1410" height="618" alt="image" src="https://github.com/user-attachments/assets/1996028e-f6de-42b6-800a-11a3ef8ef4ce" />



**Question 3**
---
<img width="1427" height="607" alt="image" src="https://github.com/user-attachments/assets/d18f1518-e689-4a7b-96d9-991377bd9c6f" />

```sql
select DoctorID,count(PrescriptionID) as TotalPrescriptions
from prescriptions
group by DoctorID;
```

**Output:**
<img width="1398" height="697" alt="image" src="https://github.com/user-attachments/assets/d47edf9f-335c-4202-a453-8df5647912a2" />



**Question 4**
---
<img width="1475" height="522" alt="image" src="https://github.com/user-attachments/assets/c6bce863-3a35-47fa-bf2e-ee03931591c4" />


```sql
select COUNT(*) as COUNT
from customer where city !='Noida';
```

**Output:**
<img width="1286" height="370" alt="image" src="https://github.com/user-attachments/assets/7ac26524-e93b-400f-97c9-4051f6d87ba6" />



**Question 5**
---
<img width="1477" height="517" alt="image" src="https://github.com/user-attachments/assets/68d9e632-6e20-4494-9110-2d58a45f3c0b" />


```sql
select count(*) as COUNT
from customer;
```

**Output:**
<img width="1327" height="368" alt="image" src="https://github.com/user-attachments/assets/166234e8-ca11-4961-8d15-93ad6466ecc2" />


**Question 6**
---
<img width="1445" height="528" alt="image" src="https://github.com/user-attachments/assets/683cc216-582e-4f2c-81fe-99f12b208304" />


```sql
select avg(income) as Average_Salary from employee;
```

**Output:**
<img width="1301" height="373" alt="image" src="https://github.com/user-attachments/assets/1b1b477e-8b45-4f25-842f-83f0d18f13ba" />



**Question 7**
---
<img width="1431" height="485" alt="image" src="https://github.com/user-attachments/assets/0ab459c4-0d47-4531-bc28-a6f256da23be" />


```sql
select sum(purch_amt) as "TOTAL" from orders;
```

**Output:**

<img width="1327" height="388" alt="image" src="https://github.com/user-attachments/assets/ba6a5e52-642a-4144-8298-39a624e9aa71" />


**Question 8**
---
<img width="1477" height="525" alt="image" src="https://github.com/user-attachments/assets/277c71c0-9de2-41b0-a109-d0806d585fa8" />

```sql
select category_id,product_name,max(price) as Price
from products
group by category_id
having max(price)>15;
```

**Output:**
<img width="1397" height="425" alt="image" src="https://github.com/user-attachments/assets/814062f9-4a8b-4cd0-b8ea-cca091472b2f" />


**Question 9**
---
<img width="1448" height="467" alt="image" src="https://github.com/user-attachments/assets/2fbf2fbf-2e1f-4f89-aa0b-980cdd2f37af" />


```sql
select (age/5)*5 as age_group,avg(age) as "AVG(age)"
from customer1
group by (age/5)*5
having avg(age)<24;
```

**Output:**
<img width="1370" height="351" alt="image" src="https://github.com/user-attachments/assets/12ccd0f6-9f6f-417e-99c1-a9ec0fad9036" />


**Question 10**
---
<img width="1441" height="488" alt="image" src="https://github.com/user-attachments/assets/ee48776e-d631-4d7b-9718-e1376b670776" />


```sql
select category_id,avg(price) as "AVG(Price)"
from products
group by category_id
having avg(price) between 10 and 15;
```

**Output:**
<img width="1376" height="405" alt="image" src="https://github.com/user-attachments/assets/048b985a-e684-4cc2-a0a0-0c9151f775bd" />

## MODULE SEB 
<img width="1850" height="785" alt="image" src="https://github.com/user-attachments/assets/86877dc4-c3cf-47aa-b9d2-05186ada41a5" />


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
