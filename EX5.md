# Ex. No: 5 Creating Triggers using PL/SQL
### DATE : 1/9/23
### AIM: To create a Trigger using PL/SQL.

### Steps:
1. Create employee table with following attributes (empid NUMBER, empname VARCHAR(10), dept VARCHAR(10),salary NUMBER);
2. Create salary_log table with following attributes (log_id NUMBER GENERATED ALWAYS AS IDENTITY, empid NUMBER,empname VARCHAR(10),old_salary NUMBER,new_salary NUMBER,update_date DATE);
3. Create a trigger named as log_salary-update.
4. Inside the trigger block, Insert the values into the salary_log table whenever the salary is updated.
5. End the trigger.
6. Update the salary of an employee in employee table.
7. Whenever a salary is updated for the employee it must be logged into the salary_log table with old salary and new salary.
8. Display the employee table, salary_log table.

### Program:

```python


CREATE TABLE s5(
  empid NUMBER,
  empname VARCHAR2(10),
  dept VARCHAR2(10),
  salary NUMBER
);

CREATE TABLE sa_log (
  log_id NUMBER GENERATED ALWAYS AS IDENTITY,
  empid NUMBER,
  empname VARCHAR2(10),
  old_salary NUMBER,
  new_salary NUMBER,
  update_date DATE
);
-- Insert the values in the employee table
insert into s5 values(1,'MUKESH','AIDS',1000000);
insert into s5 values(2,'SHREE','CSE',500000);

CREATE OR REPLACE TRIGGER log_sa_update
BEFORE UPDATE ON s5
FOR EACH ROW
BEGIN
  IF :OLD.salary != :NEW.salary THEN
    INSERT INTO sa_log (empid, empname, old_salary, new_salary, update_date)
    VALUES (:OLD.empid, :OLD.empname, :OLD.salary, :NEW.salary, SYSDATE);
  END IF;
END;
/
UPDATE s5
SET salary = 60000
WHERE empid = 1;
SELECT * FROM s5;
SELECT * FROM sa_log;


```
### Output:
![image](https://github.com/SAKTHISWAR/Ex-No-5-Creating-Triggers-using-PL-SQL/blob/main/1.jpeg)

### Result:
Thus the program to create a Trigger using PL/SQL is implemented successfully.
