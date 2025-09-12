The Case



```mysql
SELECT emp_no, first_name, last_name
	CASE
		WHEN gender = 'M' THEN 'Male'
		ELSE 'Female'
	END AS gender
FROM employees;
```
*This returns the normal three columns but 'M' values in the gender column are shown as 'Male', and all other values in gender are shown as 'Female'. It can also be simplified to the query below:*
```mysql
SELECT emp_no, first_name, last_name
	CASE
		WHEN 'M' THEN 'Male'
		ELSE 'Female'
	END AS gender
FROM employees;
```
*We know the only value containing only 'M' or 'F' is gender, which is constrained by ENUM to only hold 'M' or 'F'.*

```mysql
SELECT e.emp_no, e.first_name, e.last_name
	CASE 
		WHEN dm.emp_no IS NOT NULL THEN 'Manager'
		ELSE 'Employee'
	END AS is_manager
FROM 
	employees e
LEFT JOIN # left join bc matches + original table & values from employees ?
	dept_manager dm ON dm.emp_no = e.emp_no;
```
*Here, we assign 'Manager' to emp_no's are also seen on the Dept_manager table. If they are not, the employee is given the label 'Employee'.*