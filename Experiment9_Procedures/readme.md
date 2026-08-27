# Experiment 9: PL/SQL – Procedures and Functions

## AIM
To understand and implement procedures and functions in PL/SQL for performing various operations such as calculations, decision-making, and looping.

---

## THEORY

PL/SQL (Procedural Language/SQL) extends SQL by adding procedural constructs like variables, conditions, loops, procedures, and functions. Procedures and functions are subprograms that help modularize the code and improve reusability.

### **Procedure**
A PL/SQL **procedure** is a subprogram that performs a specific action. It does not return a value directly but can return values using `OUT` parameters.

**Syntax:**
```sql
CREATE OR REPLACE PROCEDURE procedure_name (parameters)
IS
BEGIN
   -- statements
END;
```

To call the procedure

```sql
EXEC procedure_name(arguments);
```

### **Function**
A PL/SQL **function** is a subprogram that returns a single value using the RETURN keyword.

```sql
CREATE OR REPLACE FUNCTION function_name (parameters)
RETURN datatype
IS
BEGIN
   -- statements
   RETURN value;
END;
```

To call the function:

```sql
SELECT function_name(arguments) FROM DUAL;
```

Key Differences:

-A procedure does not return a value, whereas a function must return a value.
-Functions can be called from SQL queries, procedures cannot (in most cases).

## 1. Write a PL/SQL Procedure to Find the Square of a Number

### Steps:
- Create a procedure named `find_square`.
- Declare a parameter to accept a number.
- Inside the procedure, compute the square of the input number.
- Use `DBMS_OUTPUT.PUT_LINE` to display the result.
- Call the procedure with a number as input.

### Program
```
CREATE OR REPLACE PROCEDURE find_square(
    num IN NUMBER
)
IS
    square NUMBER;
BEGIN
    square := num * num;
    DBMS_OUTPUT.PUT_LINE('Square of ' || num || ' is ' || square);
END;
/
```
### Execution
```
BEGIN
    find_square(6);
END;
/
```
**Output:**  
<img width="428" height="42" alt="image" src="https://github.com/user-attachments/assets/4f008eb2-d50e-4233-ad19-3f131cf2926e" />

---

## 2. Write a PL/SQL Function to Return the Factorial of a Number

### Steps:
- Create a function named `get_factorial`.
- Declare a parameter to accept a number.
- Use a loop to calculate the factorial.
- Return the result using the `RETURN` statement.
- Call the function using a `SELECT` statement or in an anonymous block.

### Program
```
CREATE OR REPLACE FUNCTION get_factorial(
    n IN NUMBER
)
RETURN NUMBER
IS
    fact NUMBER := 1;
BEGIN
    FOR i IN 1..n LOOP
        fact := fact * i;
    END LOOP;

    RETURN fact;
END;
/
```
### Execution
```
SELECT get_factorial(5) AS FACTORIAL
FROM DUAL;
```
**Output:**  
<img width="428" height="102" alt="image" src="https://github.com/user-attachments/assets/37b61b28-a14d-47a2-a5c5-0f43ca96fcc3" />


---

## 3. Write a PL/SQL Procedure to Check Whether a Number is Even or Odd

### Steps:
- Create a procedure named `check_even_odd`.
- Accept an input parameter.
- Use the `MOD` function to check if the number is divisible by 2.
- Display whether it is Even or Odd using `DBMS_OUTPUT.PUT_LINE`.

### Program
```
CREATE OR REPLACE PROCEDURE check_even_odd(
    num IN NUMBER
)
IS
BEGIN
    IF MOD(num,2) = 0 THEN
        DBMS_OUTPUT.PUT_LINE(num || ' is Even');
    ELSE
        DBMS_OUTPUT.PUT_LINE(num || ' is Odd');
    END IF;
END;
/
```
### Execution
```
BEGIN
    check_even_odd(12);
END;
/
```
**Output:**  
<img width="433" height="35" alt="image" src="https://github.com/user-attachments/assets/94d061df-35a8-4861-b4cf-e0b06244fe1c" />


---

## 4. Write a PL/SQL Function to Return the Reverse of a Number

### Steps:
- Create a function named `reverse_number`.
- Accept an input number as parameter.
- Use a loop to reverse the digits of the number.
- Return the reversed number.
- Call the function and display the output.

### Program
```
CREATE OR REPLACE FUNCTION reverse_number(
    num IN NUMBER
)
RETURN NUMBER
IS
    n NUMBER;
    rev NUMBER := 0;
BEGIN
    n := num;

    WHILE n > 0 LOOP
        rev := rev * 10 + MOD(n,10);
        n := TRUNC(n/10);
    END LOOP;

    RETURN rev;
END;
/
```
### Execution
```
SELECT reverse_number(1234) AS REVERSED_NUMBER
FROM DUAL;
```
**Output:**  
<img width="420" height="85" alt="image" src="https://github.com/user-attachments/assets/a51842e4-72fd-4309-b819-163d80fa6fa8" />

---

## 5. Write a PL/SQL Procedure to Display the Multiplication Table of a Number

### Steps:
- Create a procedure named `print_table`.
- Accept an input number.
- Use a loop from 1 to 10 to multiply the input number.
- Display the multiplication results using `DBMS_OUTPUT.PUT_LINE`.

### Program
```
CREATE OR REPLACE PROCEDURE print_table(
    num IN NUMBER
)
IS
BEGIN
    DBMS_OUTPUT.PUT_LINE('Multiplication Table of ' || num);

    FOR i IN 1..10 LOOP
        DBMS_OUTPUT.PUT_LINE(num || ' x ' || i || ' = ' || (num * i));
    END LOOP;
END;
/
```
### Execution
```
BEGIN
    print_table(5);
END;
/
```
**Output:**  
<img width="667" height="247" alt="image" src="https://github.com/user-attachments/assets/31d69d9c-f315-4ff4-85c9-d8e7dc353227" />


## RESULT
Thus, the PL/SQL programs using procedures and functions were written, compiled, and executed successfully.
