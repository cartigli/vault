The Case

```mysql
SELECT emp_no, first_name, last_name,
	CASE
		WHEN gender = 'M' THEN 'Male'
		ELSE 'Female'
	END AS gender
FROM employees;
```
*This returns the normal three columns but 'M' values in the gender column are shown as 'Male', and all other values in gender are shown as 'Female'. It can also be simplified to the query below:*
```mysql
SELECT emp_no, first_name, last_name,
	CASE
		WHEN 'M' THEN 'Male'
		ELSE 'Female'
	END AS gender
FROM employees;
```
*We know the only value containing only 'M' or 'F' is gender, which is constrained by ENUM to only hold 'M' or 'F'.*

```mysql
SELECT e.emp_no, e.first_name, e.last_name,
	CASE 
		WHEN dm.emp_no IS NOT NULL THEN 'Manager'
		ELSE 'Employee'
	END AS is_manager
FROM 
	employees e
LEFT JOIN # left join bc matches + original table & values from employees ?
	dept_manager dm ON dm.emp_no = e.emp_no;
```
*Here, we assign 'Manager' to emp_no's are also seen on the Dept_manager table. If they are not, the employee is given the label 'Employee'. Although, the same result could be obtained using an If clause.*
```mysql
SELECT emp_no, first_name, last_name,
	IF(gender = 'M', 'Male', 'Female') AS gender
FROM employees;
```
*The limitation of If clauses is they are restricted to one conditional expression. Cases can have multiple:*
```mysql
SELECT e.first_name, e.last_name, MAX(s.salary) - MIN(s.salary) AS sal_diff,
	CASE
		WHEN  MAX(s.salary) - MIN(s.salary) > 30000 THEN 'Salary was increased by more than 30 grand.'
		WHEN  MAX(s.salary) - MIN(s.salary) BETWEEN 20000 AND 30000 THEN 'Salary increased by 20 - 30 grand.'
		ELSE 'Salary increased less than 20 grand.'
	END AS salary_increase
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
GROUP BY s.emp_no;
```

""Retrieve the employee number (emp_no), first name (first_name), and last name (last_name) of all employees from the employees table whose employee number is greater than 10005. Join this information with the data from the department manager dept_manager table to add a fourth column named is_manager, containing the string 'Manager' if the employee number of the given employee is not a null value, and 'Employee' otherwise.""
```mysql
SELECT e.emp_no, e.first_name, e.last_name,
        CASE 
            WHEN dm.emp_no IS NOT NULL THEN 'Manager'
                ELSE 'Employee'
        END AS is_manager
FROM employees e
LEFT JOIN dept_manager dm ON dm.emp_no = e.emp_no
WHERE e.emp_no > 10005;
```
*I don't really like their examples and don't think they demonstrate the tool at hand well, or logically call for it at all.*