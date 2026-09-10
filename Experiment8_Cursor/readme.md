# Experiment 8: PL/SQL Cursor Programs

## AIM
To write and execute PL/SQL programs using cursors and exception handling to manage runtime errors effectively and display appropriate messages.

## THEORY

In PL/SQL, cursors are used to handle query result sets row-by-row. 

There are two types of cursors:

- Implicit Cursors: Automatically created by PL/SQL for single-row queries.
- Explicit Cursors: Declared and controlled by the programmer for multi-row queries.

Types of Explicit Cursors:

1. Simple Cursor: Basic cursor to iterate over multiple rows.

2. Parameterized Cursor: Accepts parameters to filter the result dynamically.

3. Cursor FOR Loop: Simplifies cursor operations (open, fetch, close).

4. %ROWTYPE Cursor: Fetches entire row into a record using %ROWTYPE.

5. Cursor with FOR UPDATE: Used for row-level locking and updating the rows while looping.

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

**Exception Handling**

PL/SQL provides a robust mechanism to handle runtime errors using exception handling blocks. When an error occurs during execution, control is passed to the EXCEPTION section, where specific or general errors can be handled gracefully.

### Components of Exception Handling:
- Predefined Exceptions: Automatically raised by PL/SQL for common errors (e.g., NO_DATA_FOUND, TOO_MANY_ROWS, ZERO_DIVIDE).
- User-defined Exceptions: Declared explicitly in the declaration section using the EXCEPTION keyword.
- WHEN OTHERS: A generic handler for all exceptions not handled explicitly.

```sql
BEGIN
   -- Statements
EXCEPTION
   WHEN exception_name THEN
      -- Handling code
   WHEN OTHERS THEN
      -- Handling for unknown errors
END;
```

### **Question 1: Simple Cursor with Exception Handling**

**Write a PL/SQL program using a simple cursor to fetch employee names and designations from the `employees` table. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: When no rows are fetched.
2. **OTHERS**: Any other unexpected errors during execution.

**Steps:**

- Create an `employees` table with fields `emp_id`, `emp_name`, and `designation`.
- Insert some sample data into the table.
- Use a simple cursor to fetch and display employee names and designations.
- Implement exception handling to catch the relevant exceptions and display appropriate messages.

### PROGRAM
```
SET SERVEROUTPUT ON;

DECLARE
    CURSOR emp_cur IS
        SELECT emp_name, designation FROM employees;

    v_name employees.emp_name%TYPE;
    v_desg employees.designation%TYPE;
    cnt NUMBER := 0;
BEGIN
    OPEN emp_cur;

    LOOP
        FETCH emp_cur INTO v_name, v_desg;
        EXIT WHEN emp_cur%NOTFOUND;

        cnt := cnt + 1;
        DBMS_OUTPUT.PUT_LINE('Employee Name : ' || v_name);
        DBMS_OUTPUT.PUT_LINE('Designation   : ' || v_desg);
    END LOOP;

    CLOSE emp_cur;

    IF cnt = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employee records found.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error: ' || SQLERRM);
END;
/
```
**Output:**  
<img width="443" height="190" alt="image" src="https://github.com/user-attachments/assets/20b6c6d2-d29a-4692-a7d1-4cde2eed7139" />


---

### **Question 2: Parameterized Cursor with Exception Handling**

**Write a PL/SQL program using a parameterized cursor to retrieve and display employees with a salary in a given range. Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees meet the salary criteria.
2. **OTHERS**: For any unexpected errors during the execution.

**Steps:**

- Modify the `employees` table by adding a `salary` column.
- Insert sample salary values for the employees.
- Use a parameterized cursor to accept a salary range as input and fetch employees within that range.
- Implement exception handling to catch and display relevant error messages.

### PROGRAM
```
SET SERVEROUTPUT ON;

DECLARE
    CURSOR emp_cur(min_sal NUMBER, max_sal NUMBER) IS
        SELECT emp_name, salary
        FROM employees
        WHERE salary BETWEEN min_sal AND max_sal;

    v_name employees.emp_name%TYPE;
    v_sal employees.salary%TYPE;
    cnt NUMBER := 0;
BEGIN
    OPEN emp_cur(30000,45000);

    LOOP
        FETCH emp_cur INTO v_name, v_sal;
        EXIT WHEN emp_cur%NOTFOUND;

        cnt := cnt + 1;
        DBMS_OUTPUT.PUT_LINE(v_name || '  Salary = ' || v_sal);
    END LOOP;

    CLOSE emp_cur;

    IF cnt = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employees found in the given salary range.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error: ' || SQLERRM);
END;
/
```
**Output:**  
<img width="450" height="83" alt="image" src="https://github.com/user-attachments/assets/a5cf6a86-57cd-4d8a-9ab6-289e8213de33" />


---

### **Question 3: Cursor FOR Loop with Exception Handling**

**Write a PL/SQL program using a cursor FOR loop to retrieve and display all employee names and their department numbers from the `employees` table. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no employees are found in the database.
2. **OTHERS**: For any other unexpected errors.

**Steps:**

- Modify the `employees` table by adding a `dept_no` column.
- Insert sample department numbers for employees.
- Use a cursor FOR loop to fetch and display employee names along with their department numbers.
- Implement exception handling to catch the relevant exceptions.

### PROGRAM
```
SET SERVEROUTPUT ON;

DECLARE
    cnt NUMBER := 0;
BEGIN
    FOR emp_rec IN (SELECT emp_name, dept_no FROM employees)
    LOOP
        cnt := cnt + 1;
        DBMS_OUTPUT.PUT_LINE('Employee: ' || emp_rec.emp_name ||
                             '  Department: ' || emp_rec.dept_no);
    END LOOP;

    IF cnt = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employees found.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error: ' || SQLERRM);
END;
/
```
**Output:**  
<img width="430" height="100" alt="image" src="https://github.com/user-attachments/assets/d04ed499-a565-486f-87b3-7f7b43c3d9c9" />


---

### **Question 4: Cursor with `%ROWTYPE` and Exception Handling**

**Write a PL/SQL program that uses a cursor with `%ROWTYPE` to fetch and display complete employee records (emp_id, emp_name, designation, salary). Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees are found in the database.
2. **OTHERS**: For any other errors that occur.

**Steps:**

- Modify the `employees` table by adding `emp_id`, `emp_name`, `designation`, and `salary` fields.
- Insert sample data into the `employees` table.
- Declare a cursor using `%ROWTYPE` to fetch complete rows from the `employees` table.
- Implement exception handling to catch the relevant exceptions and display appropriate messages.

### PROGRAM
```
SET SERVEROUTPUT ON;

DECLARE
    CURSOR emp_cur IS
        SELECT * FROM employees;

    emp_rec employees%ROWTYPE;
    cnt NUMBER := 0;
BEGIN
    OPEN emp_cur;

    LOOP
        FETCH emp_cur INTO emp_rec;
        EXIT WHEN emp_cur%NOTFOUND;

        cnt := cnt + 1;

        DBMS_OUTPUT.PUT_LINE(
            emp_rec.emp_id || '  ' ||
            emp_rec.emp_name || '  ' ||
            emp_rec.designation || '  ' ||
            emp_rec.salary
        );
    END LOOP;

    CLOSE emp_cur;

    IF cnt = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employee records found.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error: ' || SQLERRM);
END;
/
```
**Output:**  
<img width="427" height="97" alt="image" src="https://github.com/user-attachments/assets/9b7ff5d2-53f9-462f-8b39-dc912355dfdd" />


---

### **Question 5: Cursor with FOR UPDATE Clause and Exception Handling**

**Write a PL/SQL program using a cursor with the `FOR UPDATE` clause to update the salary of employees in a specific department. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no rows are affected by the update.
2. **OTHERS**: For any unexpected errors during execution.

**Steps:**

- Modify the `employees` table to include a `dept_no` and `salary` field.
- Insert sample data into the `employees` table with different department numbers.
- Use a cursor with the `FOR UPDATE` clause to lock the rows of employees in a specific department and update their salary.
- Implement exception handling to handle `NO_DATA_FOUND` or other errors that may occur.

### PROGRAM
```
SET SERVEROUTPUT ON;

DECLARE
    CURSOR emp_cur IS
        SELECT emp_id, salary
        FROM employees
        WHERE dept_no = 10
        FOR UPDATE;

    v_id employees.emp_id%TYPE;
    v_sal employees.salary%TYPE;
    cnt NUMBER := 0;
BEGIN
    OPEN emp_cur;

    LOOP
        FETCH emp_cur INTO v_id, v_sal;
        EXIT WHEN emp_cur%NOTFOUND;

        cnt := cnt + 1;

        UPDATE employees
        SET salary = salary + 5000
        WHERE CURRENT OF emp_cur;

        DBMS_OUTPUT.PUT_LINE('Updated Salary for Employee ID ' || v_id);
    END LOOP;

    CLOSE emp_cur;

    COMMIT;

    IF cnt = 0 THEN
        RAISE NO_DATA_FOUND;
    END IF;

EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employees found in the specified department.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Error: ' || SQLERRM);
END;
/
```
**Output:**  
<img width="427" height="56" alt="image" src="https://github.com/user-attachments/assets/96d19b13-e7ab-461a-88dd-c13ae8835615" />

---

## RESULT
Thus, the program successfully executed and displayed employee details using a cursor. 

