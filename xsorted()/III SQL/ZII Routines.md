A statement or set of statements stored on the SQL server. It is like a shortcut for a commonly run query.

This section feels under-utilized and could be clarified. Also, the examples used poorly demonstrated the power of these tools, so I would like an independent lesson regardless.

[ Stored Procedures ]

Semi-colons function as statement terminators, also called Delimiters. If one ran:
```mysql
DELIMITER $$
```
*'`$$`' is now your delimiter. The semi-colon is no longer your delimiter. You could also use '`//`' in place of '`$$`'.*

This is done for long procedure configurations. Within this procedure, there will be several statements. If we had four statements and tried to run this procedure, the execution would stop after the initial delimiter was found { at the end of the first statement }. To prevent early statement termination, adding a temporary delimiter like '`$$`'  allows the procedure to execute completely.
```mysql
DELIMITER $$
CREATE PROCEDURE procedure_name()
```
*Parameters represent certain values that the procedure will use to complete the calculation it is supposed to execute. Procedures can be created without Parameters, but parenthesis are always needed:*
```mysql
DELIMITER $$
CREATE PROCEDURE procedure_name (param_1, param_2)
```
*The body of a procedure is always surrounded by Begin and End clauses. This body is also always a query.*
```mysql
DELIMITER $$
CREATE PROCEDURE procedure_name (param_1, param_2)
BEGIN
	SELECT * FROM table_name
	LIMIT 1000;
END $$
```
*Please note that we use the semi-colon delimiter, not the chosen representative { '`$$`' for this case }.*

*Finishing the statement with this clause below removes the delimiter functionality of the '`$$`' delimiter:*
```mysql
DELIMITER ;
```
*To call a stored procedure, the syntax below is used:*
```mysql
CALL database_name.procedure_name();
```
*The parenthesis are not strictly necessary here and are only included for clarity.*

""Create a stored procedure that retrieves the first 1000 employees from the employees table.""
```mysql
DROP PROCEDURE IF EXISTS select_employees;

DELIMITER $$
CREATE PROCEDURE select_employees()
BEGIN
	SELECT * FROM employees
	LIMIT 1000;
END$$

DELIMITER ;
```
*Make sure the delimiter is reset to ';' after the procedure's definition, and the inner function of the procedure uses the ';'  as well as the ending the outer function with the temporary delimiter '`$$`'.*

To call this stored procedure:
```mysql
CALL employees.select_employees();
```
*Or, if already specified the database with: 'USE employees', the employees database specification of the database to use is not needed:*
```mysql
USE employees;

CALL select_employees();
```


A stored procedure can take an input Value and use it in the query, or queries, written in the body of the procedure. This value is represented by the In parameter.
```mysql
DELIMITER $$

CREATE PROCEDURE procedure_name(IN parameter)
BEGIN
	SELECT * FROM employees
	LIMIT 1000;
END $$

DELIMITER ;
```

Assume you want a first_name, last_name, salary, from_date and to_date of whichever employee you choose:
```mysql
USE employees;

DROP PROCEDURE IF EXISTS emp_salary;

DELIMITER $$
USE employees $$
CREATE PROCEDURE emp_salary(IN p_emp_no INTEGER) # name and datatype
BEGIN
SELECT e.first_name, e.last_name, s.salary, s.from_date, s.to_date
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE e.emp_no = p_emp_no
GROUP BY e.emp_no, e.first_name, e.last_name;
END $$

DELIMITER ;
```
*The procedure above uses a variable p_emp_no which is an INT to obtain its parameters. When the function is called, one must offer the procedure a value to fill for p_emp_no, like below:*
```mysql
CALL emp_salary(11300);
```

Stored Procedures can also have Aggregate Functions if they contain only one parameter:
```mysql
USE employees;

DROP PROCEDURE IF EXISTS emp_av_salary;

DELIMITER $$
USE employees $$
CREATE PROCEDURE emp_salary(IN p_emp_no INTEGER) # name and datatype
BEGIN
SELECT e.first_name, e.last_name, AVG(s.salary)
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE e.emp_no = p_emp_no;
END $$

DELIMITER ;
```
*Returns error when in group_add mode on MySQL.*
```mysql
CALL emp_av_salary(11300);
```

Stored Procedures can also have output parameters.
If the outcome needs to be stored and used as a variable within the database, an out parameter is needed.
```mysql
DELIMITER $$

CREATE PROCEDURE procedure_name(in parameter, out parameter)
BEGIN
	SELECT * FROM employees
	LIMIT 1000;
END $$

DELIMITER ;
```

```mysql
USE employees;

DROP PROCEDURE IF EXISTS emp_av_salary;

DELIMITER $$

CREATE PROCEDURE emp_av_sal_out(IN p_emp_no INTEGER, OUT p_avg_salary DECIMAL(10,2)) # why define this but only integer for input?
BEGIN SELECT AVG(s.salary)
INTO p_avg_salary FROM employees e # insert INTO OUT parameter
JOIN salaries s ON e.emp_no = s.emp_no
WHERE e.emp_no = p_emp_no;
END $$

DELIMITER ;
```
*Anytime a procedure with an in and out parameter is created, you must use the Select Into structure in the query of this object's body.*
```mysql
CALL emp_av_sal_out(11300,@p_avg_salary);
```


Stored Functions
Like a procedure but slightly modified syntax and abilities.

```mysql
DELIMITER $$

CREATE FUNCTION function_name(parameter data_type) RETURNS data_type
DECLARE variable_name data_type
BEGIN SELECT ...
RETURN variable_name
END $$

DELIMITER ;
```
*No out parameters are Out, they are only In and therefore need to specification. Although no Out's, there are Returns which have a similar purpose.
```mysql
USE employees;
DROP FUNCTION IF EXISTS f_emp_av_sal;
DELIMITER $$


CREATE FUNCTION f_emp_av_sal (v_avg_salary INTEGER) RETURNS DECIMAL(10,2)
BEGIN 

DECLARE v_avg_salary DECIMAL(10,2); # must match the RETURNS data type

SELECT AVG(s.salary) INTO v_avg_salary
FROM employees e
JOIN salaries s 
	ON e.emp_no = s.emp_no
WHERE 
	e.emp_no = v_avg_salary;
RETURN v_avg_salary;

END $$

DELIMITER ;
```