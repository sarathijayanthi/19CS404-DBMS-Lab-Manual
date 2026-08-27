# Experiment 7: PL/SQL – Variables, Control Structures and Loops

## AIM
To write and execute simple PL/SQL programs using variables, loops, and conditional statements.


## THEORY

PL/SQL, which stands for Procedural Language extensions to the Structured Query Language (SQL). It is a combination of SQL along with the procedural features of programming languages.

**Syntax:**
```sql
DECLARE 
   <declarations section> 
BEGIN 
   <executable command(s)>
EXCEPTION 
   <exception handling> 
END;
```

### Basic Components of PL/SQL Block:
- DECLARE: Section to declare variables and constants.
- BEGIN: The execution section that contains PL/SQL statements.
- EXCEPTION: Handles errors or exceptions that occur in the program.
- END: Marks the end of the PL/SQL block.

# PL/SQL Programs – Steps and Expected Output

## 1. Write a PL/SQL program to find the Greatest of Two Numbers

### Steps:
- Declare two numeric variables and initialize them.
- Use an `IF` statement to compare the values.
- Display the greater number using `DBMS_OUTPUT.PUT_LINE`.
  
### Program
 ```
SET SERVEROUTPUT ON;

DECLARE
    a NUMBER := 50;
    b NUMBER := 80;
BEGIN
    IF a > b THEN
        DBMS_OUTPUT.PUT_LINE('Greater number is: ' || a);
    ELSE
        DBMS_OUTPUT.PUT_LINE('Greater number is: ' || b);
    END IF;
END;
/
``` 

**Output:**  

<img width="472" height="67" alt="image" src="https://github.com/user-attachments/assets/75ee9b9b-10bb-42a4-bc3e-ab19b3039de5" />


## 2. Write a PL/SQL program to Calculate Sum of First N Natural Numbers

### Steps:
- Declare a variable `n` and assign a value (e.g., 10).
- Initialize a `sum` variable to 0.
- Use a `WHILE` loop to iterate from 1 to `n`, adding each number to the sum.
- Display the result using `DBMS_OUTPUT.PUT_LINE`.
  
### Program  
```
SET SERVEROUTPUT ON;

DECLARE
    n NUMBER := 10;
    i NUMBER := 1;
    sum NUMBER := 0;
BEGIN
    WHILE i <= n LOOP
        sum := sum + i;
        i := i + 1;
    END LOOP;

    DBMS_OUTPUT.PUT_LINE('Sum of first ' || n || ' natural numbers is: ' || sum);
END;
/
```
**Output:**  
<img width="490" height="73" alt="image" src="https://github.com/user-attachments/assets/d371718d-a678-4057-8c1e-72672b961d5f" />


---

## 3. Write a PL/SQL program to generate Fibonacci series

### Steps:
- Declare the variable `n` to indicate how many terms to generate.
- Initialize the first two Fibonacci numbers (0 and 1).
- Use a loop to generate the next terms using the formula `c = a + b`.
- Print each term in the series.

### Program
```
SET SERVEROUTPUT ON;

DECLARE
    n NUMBER := 7;
    a NUMBER := 0;
    b NUMBER := 1;
    c NUMBER;
    i NUMBER := 3;
BEGIN
    DBMS_OUTPUT.PUT_LINE('Fibonacci sequence:');
    DBMS_OUTPUT.PUT_LINE(a);
    DBMS_OUTPUT.PUT_LINE(b);

    WHILE i <= n LOOP
        c := a + b;
        DBMS_OUTPUT.PUT_LINE(c);
        a := b;
        b := c;
        i := i + 1;
    END LOOP;
END;
/
```
**Output:**  
<img width="677" height="197" alt="image" src="https://github.com/user-attachments/assets/1c33a731-c887-455e-a8f2-e5777b5acab8" />

---

## 4. Write a PL/SQL Program to display the number in Reverse Order

### Steps:
- Declare a variable `n` and assign a value (e.g., 1535).
- Use a loop to extract each digit using modulo and reverse the number.
- Display the reversed number.

### Program
```
SET SERVEROUTPUT ON;

DECLARE
    n NUMBER := 1535;
    rev NUMBER := 0;
    rem NUMBER;
    temp NUMBER;
BEGIN
    temp := n;

    WHILE temp > 0 LOOP
        rem := MOD(temp, 10);
        rev := rev * 10 + rem;
        temp := TRUNC(temp / 10);
    END LOOP;

    DBMS_OUTPUT.PUT_LINE('Original Number: ' || n);
    DBMS_OUTPUT.PUT_LINE('Reversed Number: ' || rev);
END;
/
```
**Output:**  
<img width="452" height="87" alt="image" src="https://github.com/user-attachments/assets/0baa7e42-720c-4384-aa6a-697d5e97b506" />


---

## 5. Write a PL/SQL program to find the largest of three numbers

### Steps:
- Declare three numeric variables `a`, `b`, and `c`.
- Use nested `IF-ELSIF-ELSE` conditions to find the largest among the three.
- Display the largest number.

### Program
```
SET SERVEROUTPUT ON;

DECLARE
    a NUMBER := 10;
    b NUMBER := 9;
    c NUMBER := 15;
BEGIN
    IF a >= b AND a >= c THEN
        DBMS_OUTPUT.PUT_LINE('Largest number is: ' || a);
    ELSIF b >= a AND b >= c THEN
        DBMS_OUTPUT.PUT_LINE('Largest number is: ' || b);
    ELSE
        DBMS_OUTPUT.PUT_LINE('Largest number is: ' || c);
    END IF;
END;
/
```
**Output:**  
<img width="435" height="55" alt="image" src="https://github.com/user-attachments/assets/b315cfb0-7925-41e2-9a2c-015e3a4a7ff4" />


## RESULT
Thus, the PL/SQL programs using variables, conditionals, and loops were executed successfully.
