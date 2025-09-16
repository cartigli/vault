""_Tackling these last five coding exercises won't demand writing the most complex queries. Instead, the challenge lies in correctly identifying the right tool to achieve the desired outcome. We only suggest a solution, but feel free to obtain the expected result in a different way. Be ready to utilize any of the MySQL tools you've learned throughout the course. Aim to complete these exercises as quickly as possible, at least on your first attempt._

Find the average salary of male and female employees in each department. The desired result set should contain three columns: department name (dept_name), gender (gender), and average salary (avg_salary). Apply only to average salary values higher than $70,000. Order your output by department number, starting with the lowest.""
```mysql
SELECT d.dept_name, e.gender, AVG(s.salary) AS avg_salary
FROM salaries s 
JOIN employees e ON e.emp_no = s.emp_no
JOIN dept_emp de ON s.emp_no = de.emp_no
JOIN departments d ON d.dept_no = de.dept_no
GROUP BY d.dept_name, e.gender
HAVING avg_salary > 70000
ORDER BY d.dept_no;
```
*Their solution:*
```mysql
1. SELECT
2. d.dept_name, e.gender, AVG(salary) AS avg_salary
3. FROM
4. salaries s
5. JOIN
6. employees e ON s.emp_no = e.emp_no
7. JOIN
8. dept_emp de ON e.emp_no = de.emp_no
9. JOIN
10. departments d ON d.dept_no = de.dept_no
11. GROUP BY de.dept_no , e.gender
12. HAVING AVG(salary) > 70000
13. ORDER BY de.dept_no;
```

""Assign 10006 (as an integer value) as manager to all employees with a number between 10001 and 10005, inclusive. Assign 10007 to all others. Apply only to employees with a number not higher than 10008. To obtain the desired result, organize your output into three columns:
1. The first column (emp_no) containing the employee number.   
2. The second column (dept_no) containing the lowest department number they have ever signed a contract for, as recorded in the (dept_emp) table.  
3. The last column (manager_no) containing the number of the manager assigned to the given employee.""
```mysql
SELECT A.*
FROM (SELECT 
    e.emp_no, 
    MIN(de.dept_no) AS dept_no,
    (
    SELECT emp_no 
    FROM dept_manager
    WHERE 
        emp_no = 10006) AS manager_no
FROM employees e
JOIN dept_emp de ON e.emp_no = de.emp_no
WHERE de.emp_no IN (10001, 10002, 10003, 10004, 10005)
GROUP BY e.emp_no
ORDER BY e.emp_no) AS A 
UNION SELECT B.*
FROM (SELECT 
        e.emp_no, 
        MIN(de.dept_no) AS dept_no,
        (
        SELECT emp_no 
        FROM dept_manager
        WHERE 
            emp_no = 10007) AS manager_no
    FROM employees e
    JOIN dept_emp de ON e.emp_no = de.emp_no
    JOIN dept_manager dm ON e.emp_no = dm.emp_no
    WHERE e.emp_no < 10009
    GROUP BY e.emp_no
    ORDER BY e.emp_no) AS B;
```
*I'm not going to lie, their solution is much better here:*
```mysql
1. SELECT
2. emp_no,
3. (SELECT
4. MIN(dept_no)
5. FROM
6. dept_emp de
7. WHERE
8. e.emp_no = de.emp_no) dept_no,
9. CASE
10. WHEN emp_no <= 10005 THEN '10006'
11. ELSE '10007'
12. END AS manager_no
13. FROM
14. employees e
15. WHERE
16. emp_no <= 10008;
```


""Retrieve all records from the `employees` table for employees hired between January 1, 1988, and December 31, 1992, inclusive.""
```mysql
SELECT * FROM employees
WHERE hire_date BETWEEN '1988-01-01' AND '1992-12-31';
```
*Their solution:*
```mysql
1. SELECT
2. *
3. FROM
4. employees
5. WHERE
6. hire_date BETWEEN '1988-01-01' AND '1993-01-01';
```


""Retrieve a list of all employees from the titles table who are staff members. Organize your output into emp_no, title, from_date, and to_date columns.""
```mysql
SELECT 
    emp_no, 
    title,
    from_date,
    to_date
FROM titles
WHERE title LIKE ('%Staff%');
```
*They done did it again:*
```mysql
1. SELECT
2. *
3. FROM
4. titles
5. WHERE
6. title LIKE ('%staff%');
```

""How many open-ended contracts with a value higher than $74,057 have been registered in the salaries table? Store your output in a column named 'num_open_ended_contracts'. Please note that open-ended contracts have all been assigned January 1, 9999 as a to_date.""
```mysql
SELECT COUNT((CASE WHEN salary > 74056 THEN 1 ELSE 0 END)) AS num_open_ended_contracts
FROM salaries
WHERE to_date = '9999-01-01' AND salary > 74057;
```
*Just in my freaking face:*
```mysql
SELECT COUNT(*) AS num_open_ended_contracts
FROM salaries
WHERE salary > 74057
AND to_date = '9999-01-01';
```