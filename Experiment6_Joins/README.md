# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--
<img width="1480" height="862" alt="image" src="https://github.com/user-attachments/assets/7dff6fa7-b5c2-497d-8be2-30e0d421719f" />


```sql
select c.cust_name as "Customer Name" ,c.city,s.name as Salesman,s.commission from customer c
inner join salesman s on c.salesman_id=s.salesman_id;
```

**Output:**
<img width="1313" height="817" alt="image" src="https://github.com/user-attachments/assets/987bc5c7-ea11-42af-87d7-aee971a679ee" />



**Question 2**
---
<img width="1482" height="657" alt="image" src="https://github.com/user-attachments/assets/923851b8-a3ec-4e14-81e5-75781eb4d17a" />


```sql
select c.cust_name,o.ord_no,o.ord_date,o.purch_amt from customer c
left join orders o on c.customer_id=o.customer_id;
```

**Output:**
<img width="1387" height="741" alt="image" src="https://github.com/user-attachments/assets/5e9c1f4d-f4bf-4e70-9a39-b826f3ab9997" />



**Question 3**
---
<img width="1493" height="703" alt="image" src="https://github.com/user-attachments/assets/8d3931c5-6525-48e2-8e66-88b5cf270697" />


```sql
select n.nurse_id,d.department_name from nurses n
inner join departments d on n.department_id=d.department_id where n.first_name="David" and n.last_name="Moore";
```

**Output:**

<img width="1337" height="452" alt="image" src="https://github.com/user-attachments/assets/14beb24f-a82f-48dd-b897-590b7c0ea557" />


**Question 4**
---
<img width="1482" height="857" alt="image" src="https://github.com/user-attachments/assets/69e1c898-9d7b-4085-89c4-a828982f2092" />


```sql
select c.cust_name,c.city,c.grade,s.name as Salesman,s.city from customer c
inner join salesman s on c.salesman_id=s.salesman_id order by c.customer_id ;
```

**Output:**
<img width="1380" height="827" alt="image" src="https://github.com/user-attachments/assets/2c781e16-d601-4e8d-941c-f45edf4de4a9" />



**Question 5**
---
<img width="1472" height="675" alt="image" src="https://github.com/user-attachments/assets/33aacde1-f5af-496c-88de-82b75a00c1af" />


```sql
select p.patient_id,p.first_name,p.last_name,p.date_of_birth,p.admission_date,p.discharge_date,p.doctor_id from patients p
inner join appointments a on p.patient_id=a.patient_id where p.admission_date between '2024-01-01' and '2024-01-31';
```

**Output:**
<img width="1365" height="457" alt="image" src="https://github.com/user-attachments/assets/2cd95bf9-9578-43b5-aa86-0aa9d1574d5e" />



**Question 6**
---
<img width="1486" height="860" alt="image" src="https://github.com/user-attachments/assets/5bc4eb45-d9d4-4e0b-a9b2-6d9de94d542c" />


```sql
select o.ord_no,o.purch_amt,c.cust_name,c.city from orders o
inner join customer c on o.customer_id=c.customer_id where o.purch_amt between 500 and 2000;
```

**Output:**
<img width="1361" height="527" alt="image" src="https://github.com/user-attachments/assets/982018bc-65ee-4afd-948b-356d9de51c41" />



**Question 7**
---
<img width="1487" height="828" alt="image" src="https://github.com/user-attachments/assets/b369aa5b-2ea6-411e-8099-8b98ef99cfd2" />

```sql
SELECT
    c.cust_name,
    c.city,
    o.ord_no,
    o.ord_date,
    o.purch_amt AS "Order Amount",
    s.name,
    s.commission
FROM customer c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
LEFT JOIN salesman s
    ON o.salesman_id = s.salesman_id;
```

**Output:**
<img width="1327" height="765" alt="image" src="https://github.com/user-attachments/assets/7fb5a381-c2b8-4007-9077-fce8f29d865d" />



**Question 8**
---
<img width="1482" height="382" alt="image" src="https://github.com/user-attachments/assets/b4f64ed5-88ea-4579-9ac2-a4dcf15e1ed5" />

```sql
select s.name from salesman s left join customer c on s.salesman_id=c.salesman_id where c.city="New York";
```

**Output:**
<img width="1335" height="462" alt="image" src="https://github.com/user-attachments/assets/89f15a88-5a6a-4028-9d5b-759fdb7dec5a" />



**Question 9**
---
<img width="1472" height="872" alt="image" src="https://github.com/user-attachments/assets/265a03e4-cba4-4dbc-9946-f747ca7b8944" />


```sql
select c.cust_name,c.city,c.grade,s.name as Salesman,s.city from customer c
inner join salesman s on c.salesman_id=s.salesman_id where c.grade<300 order by customer_id;
```

**Output:**
<img width="1386" height="722" alt="image" src="https://github.com/user-attachments/assets/64c04d25-a8c8-4e47-9b23-ef2a67ba2151" />



**Question 10**
---
<img width="1481" height="775" alt="image" src="https://github.com/user-attachments/assets/61bdd4b0-7cd6-417d-b565-5b3360b008b3" />

```sql
select p.first_name from patients p inner join surgeries s on p.patient_id=s.patient_id where s.surgery_date="2024-01-15";
```

**Output:**
<img width="1356" height="477" alt="image" src="https://github.com/user-attachments/assets/14125fa0-3af6-43f4-8942-3cd060226dd3" />

## MODULE- SEB
<img width="1917" height="706" alt="image" src="https://github.com/user-attachments/assets/7b90d4bb-8d81-4cd6-9dda-e56b523a7b28" />


## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
