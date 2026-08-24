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
<img width="1478" height="632" alt="image" src="https://github.com/user-attachments/assets/daced396-e893-46d8-a1a2-6ac145eb2f9d" />


```sql
SELECT *
FROM CUSTOMERS
WHERE ADDRESS = 'Delhi'
  AND AGE < 30 ORDER BY ID;
```

**Output:**
<img width="1367" height="417" alt="image" src="https://github.com/user-attachments/assets/476da29b-9689-482c-af94-f30c297f9ae3" />



**Question 2**
---
<img width="1486" height="635" alt="image" src="https://github.com/user-attachments/assets/b38e8b4d-9029-4dfd-8e96-5bdab9381fce" />


```sql
SELECT *
FROM GRADES g
WHERE grade = (
    SELECT MIN(grade)
    FROM GRADES
    WHERE subject = g.subject
);
```

**Output:**

<img width="1323" height="457" alt="image" src="https://github.com/user-attachments/assets/3eef1d81-1d2b-4844-b527-26c1c5ba02e9" />


**Question 3**
---
<img width="1495" height="801" alt="image" src="https://github.com/user-attachments/assets/87cd9d3b-2197-4639-85d3-9243600e4f3b" />


```sql
SELECT
    ord_no,
    purch_amt,
    ord_date,
    customer_id,
    orders.salesman_id
FROM orders
JOIN salesman
ON orders.salesman_id = salesman.salesman_id
WHERE salesman.city = 'New York';
```

**Output:**
<img width="1327" height="507" alt="image" src="https://github.com/user-attachments/assets/ce24fd3d-d67b-4e09-9ec9-8d35b52aef2d" />


**Question 4**
<img width="1520" height="730" alt="image" src="https://github.com/user-attachments/assets/6bb445c0-c6e2-43b6-8f47-85fbcb1c3d28" />


```sql
SELECT
    ord_no,
    purch_amt,
    ord_date,
    customer_id,
    orders.salesman_id
FROM orders
JOIN salesman
ON orders.salesman_id = salesman.salesman_id
WHERE salesman.name = 'Paul Adam';
```

**Output:**
<img width="1382" height="460" alt="image" src="https://github.com/user-attachments/assets/7536c7f6-4a92-4a38-b8fa-979291f000bb" />


**Question 5**
---
<img width="1497" height="676" alt="image" src="https://github.com/user-attachments/assets/f99d5d34-f9c8-4c2a-a7f0-b8c29739a45c" />


```sql
SELECT DISTINCT commission
FROM salesman
WHERE salesman_id IN (
    SELECT salesman_id
    FROM customer
    WHERE city = 'Paris'
);
```

**Output:**
<img width="1340" height="405" alt="image" src="https://github.com/user-attachments/assets/bcb050a3-0d5a-428f-9455-fd93163d2457" />



**Question 6**
---
<img width="1491" height="621" alt="image" src="https://github.com/user-attachments/assets/f66cdc66-f7fd-415c-8178-ed5ec7f82a8d" />


```sql
SELECT student_name, grade
FROM GRADES g
WHERE grade = (
    SELECT MAX(grade)
    FROM GRADES
    WHERE subject = g.subject
);
```

**Output:**
<img width="1321" height="437" alt="image" src="https://github.com/user-attachments/assets/0d390755-baef-4da3-9d50-6a3996dcde1c" />



**Question 7**
---
<img width="1500" height="791" alt="image" src="https://github.com/user-attachments/assets/985ac2e3-03ce-4009-a2f6-8a058963f4d5" />


```sql
SELECT
    o.ord_no,
    o.purch_amt,
    o.ord_date,
    o.salesman_id
FROM orders o
JOIN salesman s
ON o.salesman_id = s.salesman_id
WHERE s.commission = (
    SELECT MAX(commission)
    FROM salesman
);
```

**Output:**
<img width="1340" height="505" alt="image" src="https://github.com/user-attachments/assets/e9025b6e-8532-4b51-ae04-262c431cecc0" />


**Question 8**
---
<img width="1510" height="518" alt="image" src="https://github.com/user-attachments/assets/ad57406e-91bd-4a29-82f8-27a5e0302b64" />

```sql
SELECT medication_id AS medic, medication_name, dosage
FROM Medications
WHERE dosage = (
    SELECT MIN(dosage)
    FROM Medications
);

```

**Output:**
<img width="1306" height="442" alt="image" src="https://github.com/user-attachments/assets/c4d4d5c9-dfc8-4c60-8bd4-e0af1c913d85" />



**Question 9**
---
<img width="1486" height="791" alt="image" src="https://github.com/user-attachments/assets/716bd80f-90e9-456e-85c9-ff5925176ec4" />


```sql
SELECT
    o.ord_no,
    o.purch_amt,
    o.ord_date,
    o.customer_id,
    o.salesman_id
FROM ORDERS o
JOIN SALESMAN s
ON o.salesman_id = s.salesman_id
WHERE s.city = 'New York';
```

**Output:**
<img width="1343" height="542" alt="image" src="https://github.com/user-attachments/assets/a317240e-b4ac-41b3-8cc6-1109d2bb2c9d" />


**Question 10**
---


<img width="1497" height="732" alt="image" src="https://github.com/user-attachments/assets/c0215201-7ca9-4422-b341-aaab7ce7e4e9" />


```sql
SELECT *
FROM CUSTOMERS
WHERE AGE < 30;
```

**Output:**

<img width="1316" height="582" alt="image" src="https://github.com/user-attachments/assets/1969fae4-945c-48d0-a06c-45ff1651954a" />

## MODULE-SEB

<img width="1916" height="588" alt="image" src="https://github.com/user-attachments/assets/9e4745f1-96e3-467a-aaf9-79ea913bbdae" />


## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
