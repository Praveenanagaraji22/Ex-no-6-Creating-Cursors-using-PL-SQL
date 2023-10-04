# Ex. No: 5 Creating Cursors using PL/SQL

### AIM: To create a cursor using PL/SQL.

### Steps:
1. Create employee table with following attributes (empid NUMBER, empname VARCHAR(10), dept VARCHAR(10),salary NUMBER);
2. Create a cursor named as employee_cursor
3. Using cursor read each record and display the result
4. Close the cursor

### Program:
### Create employee table
#### Query:
```
CREATE TABLE employee (empid INT,empname VARCHAR(10),dept VARCHAR(10),salary DECIMAL(10, 2));

INSERT INTO employee VALUES (1, 'Abi', 'Sales', 100000);
INSERT INTO employee VALUES (2, 'Divya', 'marketing', 120000);

select * from employee;
```
#### Table:
![1](https://github.com/Divya110205/Ex-no-6-Creating-Cursors-using-PL-SQL/assets/119404855/008b9148-cd74-4e60-8f82-61c94093645e)

### PLSQL Cursor code
```
DELIMITER //

CREATE PROCEDURE fetch_employee_data()
BEGIN
  DECLARE v_empid INT;
  DECLARE v_empname VARCHAR(10);
  DECLARE v_dept VARCHAR(10);
  DECLARE v_salary DECIMAL(10, 2);
  
  DECLARE employee_cursor CURSOR FOR SELECT empid, empname, dept, salary FROM employee;
  
  DECLARE CONTINUE HANDLER FOR NOT FOUND SET @finished = 1;
  
  OPEN employee_cursor;
  
  SET @finished = 0;
  
  FETCH_NEXT: LOOP
    FETCH employee_cursor INTO v_empid, v_empname, v_dept, v_salary;
    IF @finished = 1 THEN
      LEAVE FETCH_NEXT; -- Exit the loop when no more rows
    END IF;

    SELECT v_empid, v_empname, v_dept, v_salary;
  END LOOP FETCH_NEXT;
  
 
  CLOSE employee_cursor;
END //

DELIMITER ;

CALL fetch_employee_data();
```
### Output:
![2](https://github.com/Divya110205/Ex-no-6-Creating-Cursors-using-PL-SQL/assets/119404855/60508395-7d88-4821-af32-7fadf3f55bbf)

### Result:
The program is implemented successfully,
