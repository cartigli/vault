MySQL Variable Types: Local, Session, and Global

Scope = region of a computer program where a phenomenon, such as a variable, is considered valid


Variables
When defining a program, such as stored procedures, ' parameters ' is an appropriate term. Whatever is given to the procedure as Input is considered an argument of the procedure, while the output of a procedure, if exists, stores the output of said procedure in a variable. It depends, or varies, based off the input for the given procedure.

Creating a variable is done with ' @ ':
```mysql
SET @p_avg_salary = 0;
```
*Initial value of the variable is not important here.*
Call the procedure to be assigned to the newly created variable
```mysql
CALL employees.emp_av_sal_out(11300, @p_avg_salary);
```
*The resulting output from the procedure named emp_av_sal_out will be stored in the variable v_avg_salary.*
```mysql
SELECT @p_av_salary;
```
*Stored Procedures can have multiple outputs while a function can only have one. Furthermore, Stored Procedures are better for things like Insert, Delete, or Update as Functions need a value to return and Insert, Update, and Delete do not return anything. Finally, Functions are referenced in a Select statement while Stored Procedures cannot be called from a Select statement.*


Local Variables
Visible only in the Begin - End block in which it was created.

```mysql
USE employees;
DROP FUNCTION IF EXISTS f_emp_av_sal;
DELIMITER $$


CREATE FUNCTION f_emp_av_sal (p_emp_no INTEGER) RETURNS DECIMAL(10,2)
BEGIN 

DECLARE p_emp_no DECIMAL(10,2); # must match the RETURNS data type

SELECT AVG(s.salary) INTO v_avg_salary 
FROM employees e
JOIN salaries s 
	ON e.emp_no = s.emp_no
WHERE 
	e.emp_no = p_emp_no;
RETURN v_avg_salary;

END $$

DELIMITER ;
```
*In this function, the declare statement is used to create this variable. Declare can only be used to create Local variables. Therefore, v_avg_salary is Local, and only viewable when between Begin and End in this function.*
	*Trying to call or Select these variables outside of the scope of this function will result in an error.*

Session Variables
Broader scope than Local variables but less so than Global variables.
A session is a series of information exchange interactions, or a dialogue, between a computer and a user. In this case, it is a dialogue between the MySQL server and a client application: Workbench.
	Sessions begin after a connection is established and the client is connected, i.e., Workbench in this case, and the session is ended when the Workbench application disconnects from the mysql.server.

Certain SQL objects are only valid for a specific session; Session Variables are one such object. They are defined on the local instance of the server and live there. It is only visible to the connection being currently used.

```mysql
SET @s_var1 = 3;
```
*Assigns the value of 3 for the variable s_var1. Selecting the variable will return 3. Opening another tab allows the same return, but opening a new collection will return an Null value if this variable is called. This new session is beyond the scope of the variable.*

Global Variables
Their scope is broader than that of Session variables. Global variables apply to all connections to a specific server.

```mysql
SET GLOBAL var_name = value;
#or 
SET @@GLOBAL.var_name = value;
```

Global variables cannot be any variable. MySQL provides the appropriate predefined variables; System Variables.

.max_connections() indicates the maximum number of connections to a server than can be established at a given point in time.
.max_join_size() sets the maximum memory space allocated for the joins created by a certain connection.

```mysql
SET GLOBAL max_connections = 1000;
```
*Limit the amount of connections of the server to 1000 connections. The query below is functionally identical to the one above.*
```mysql
SET @@GLOBAL.max_connections = 1000;
```


User Defined vs System Variables$$\begin{array} \\
\text{Variable Types} & \text{Local Variables} & \text{Session Variables} & \text{Global Variables}\\
\text{User Defined} & \checkmark & \checkmark & X \\
\text{System} & X & \checkmark & \checkmark \\
\end{array}$$

"Create a variable named `v_emp_no` containing the integer 10004. Retrieve the employee number, first name, last name, and hire date of the employee with the employee number stored in `v_emp_no`. To obtain the desired output, use the data from the employees table."
```mysql
SET @v_emp_no = 10004;

SELECT e.emp_no, e.first_name, e.last_name, e.hire_date
FROM employees e
WHERE e.emp_no = @v_emp_no;
```


MySQL Triggers
A type of stored program, associated with a table, that will be activated once some condition or event occurs.
	This event must be related to the associated table and represented by one of the following DML statements: INSERT, UPDATE, or DELETE.

A Trigger is a MySQL object that can ' trigger ' a specific action or calculation ' before ' or ' after ' an Insert, Update, or Delete statement has been executed.

Like System Variables, MySQL also has predefined System Functions which provide data about the moment of the execution of a given query.

Obviously there are immeasurable amounts of uses for this ability, but here's a simple one:
	A new employee is promoted to manager. This employee's salary should immediately increase by $20,000 and a record should be added to the dept_manager table. Additionally, start & from dates must be modified, the salaries table will need adjustment, the dept_manager table will need to know who is under this employee, etc., etc.



Before Insert Trigger

In this example, we'll begin with a commit execution to ensure we can rollback the changes.
```mysql
USE employees;

COMMIT;

DELIMITER $$

CREATE TRIGGER before_salaries_insert
BEFORE INSERT ON salaries
FOR EACH ROW
BEGIN
	IF NEW.salary < 0 THEN # if new salary is negative, then
		SET NEW.salary = 0; # set it equal to 0
	END IF; # end conditional
END$$

DELIMITER ;
```
*New refers to a New record being inserted. Set assigns the newly inserted value as 0 if its value is negative.*
After committing and executing, let's give the salaries table a negative value and observe the results:
```mysql
INSERT INTO salaries VALUES ('10001',-92891, '2010--06-22', '9999-01-01')

SELECT * FROM salaries
WHERE emp_no = '10001'
```
*In return, we get the same table as before with one additional row, shown with a salary of 0 among the other values we Inserted, meaning the Insert Trigger was correctly activated and accurately executed its query.*

Before Update Trigger
```mysql
USE employees;

DELIMITER $$

CREATE TRIGGER before_salaries_insert
BEFORE UPDATE ON salaries
FOR EACH ROW
BEGIN
	IF NEW.salary < 0 THEN # if new salary is negative, then
		SET NEW.salary = OLD.salary; # reset the salary to the previous value
	END IF; # end conditional
END$$

DELIMITER ;
```
*Currently, emp_no 10001 has a salary of 0. Let's update it.*
```mysql
UPDATE salaries 
SET salary = 98765
WHERE emp_no = '10001'
AND from_date = '2010-06-22';
```
*Now their salary is $98,765; Updating with a positive number changed their salary. Let's try a negative.*
```mysql
UPDATE salaries
SET salary = -98765
WHERE emp_no = '10001'
AND from_date = '2010-06-22';
```
*Salary did not change from $98,765; the Update Trigger operated as intended and set the salary back to the previous value because we tried to update to a negative number. Considering our rule, we should be able to set the salary to 0. Let's try.
```mysql
UPDATE salaries
SET salary = 0
WHERE emp_no = '10001'
AND from_date = '2010-06-22';
```
*Yes! His salary is back to $0 and our trigger works as intended. We'll get emp_no 10001 next time.*


System Functions
System Functions give information about the time and manner of an execution.

```mysql
SELECT SYSDATE();
```
*Shows / returns the current date of the given query's execution. You can receive only specified portions of the current date with the syntax below:*
```mysql
SELECT DATE_FORMAT(SYSDATE()), '%y-%m-%d') AS today;
```
*This returns the date in the format: YY-MM-DD. Sysdate() alone includes the time in HH-MM-SS.*


"Someone has been promoted from employee to manager. Their annual salary should be $20,000 higher than the highest salary they've earned to date and the Dept_manager table will need updating." 
	Let's create a trigger that applies several modifications to the Salaries table once the relevant record is inserted into the Dept_manager table which will:
			Ensure the end date of the previous highest salary contract of that employee is the one from the execution of the insert statement { we assume the highest salary they have earned is the latest one & we can use the Sysdate function to get the end date for said salary }
			Insert into Salaries a new record where:
					a start date equal to the new from date from the newly inserted record in Dept_manager
					a salary equal to their highest ever salary plus $20,000
					a contract of indefinite duration, i.e., ending on the date 9999-01-01

```mysql
USE employees;

DELIMITER $$

CREATE TRIGGER trig_ins_dept_mng
AFTER INSERT ON dept_manager
FOR EACH ROW
BEGIN
	DECLARE v_curr_salary INTEGER;
	SELECT MAX(salary)
	INTO v_curr_salary FROM
		salaries
	WHERE emp_no = NEW.emp_no; # find this salary for the emp_no that was newly inserted intp the dept_table 
	IF v_curr_salary IS NOT NULL THEN
		UPDATE salaries
		SET
			to_date = SYSDATE()
		WHERE
			emp_no = NEW.emp_no AND to_date = NEW.to_date;

		INSERT INTO salaries
			VALUES(NEW.emp_no, v_curr_salary + 20000, NEW.from_date, NEW.to_date);
	END IF;
END $$

DELIMITER ;
```

```mysql
INSERT INTO dept_manager VALUES('111534','d009',date_format(sysdate(), '%y-%m-%d'), '9999-01-01');

SELECT * FROM salaries
WHERE emp_no = '111534';
```