# Ex. No: 5 Creating Triggers using PL/SQL
## Date: 1/9/23
### AIM: 
  To create a Trigger using PL/SQL.

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
### Create employee table
```

SQL> CREATE TABLE e2(
     empid NUMBER,
     empname VARCHAR2(10),
     dept VARCHAR2(10),
     salary NUMBER
     );
```
![emptbl](https://github.com/abinayasangeetha/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119393675/a619ffd1-8edf-4e3d-b98f-2c99e484344d)

### Create salary_log table
```
SQL> CREATE TABLE wages_log1
     (
     log_id NUMBER GENERATED ALWAYS AS IDENTITY,
     empid NUMBER,
     empname VARCHAR2(10),
     old_salary NUMBER,
     new_salary NUMBER,
     update_date DATE
     );
```
![wglogtbl](https://github.com/abinayasangeetha/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119393675/a2b739a5-1b83-423e-a40c-34790df49d3d)

###  Inserting data into the employed table:
```
insert into e2 values(1,'Divya','IT',100000);
insert into e2 values(2,'ABINAYA','SALES',50000);
insert into e2 values(3,'RANBIR','HR',110000);
insert into e2 values(4,'RANVEER','SALES',50000);
insert into e2 values(5,'VARUN','IT',100000);
```
![insertval](https://github.com/abinayasangeetha/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119393675/ee9a6a0d-6ea4-40c1-bb4d-397de68ecbe4)
![insertval2](https://github.com/abinayasangeetha/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119393675/22c22c29-4153-4f53-9108-f33525bca4e3)

### Update the salary of an employed:
```
UPDATE e2
SET salary = 120000
where empid=3;
```
![update](https://github.com/abinayasangeetha/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119393675/51ccdd5d-6509-4e6d-9556-3bf43bba4c17)

### PLSQL Trigger code

```
SQL> CREATE OR REPLACE TRIGGER loggingg_sal_update
     BEFORE UPDATE ON e2
     FOR EACH ROW
     BEGIN
     IF :OLD.salary != :NEW.salary THEN
     INSERT INTO  wages_log1 (empid, empname, old_salary, new_salary, update_date)
     VALUES (:OLD.empid, :OLD.empname, :OLD.salary, :NEW.salary, SYSDATE);
     END IF;
     END;
     /
```
![trigger sql](https://github.com/abinayasangeetha/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119393675/33bb473f-4aaf-4d38-b582-38c5e2b7c9b2)

### Output:
![opdbms5](https://github.com/abinayasangeetha/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119393675/169193c8-fecc-4cfd-8e1a-7ab9010d6d48)

### Result:
 To create a Trigger using PL/SQL is executed successfully.
