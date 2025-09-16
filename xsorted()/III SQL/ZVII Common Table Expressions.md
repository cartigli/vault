In MySQL, queries and some parts of queries and subprocess produces a temporary dataset, or a result.
	A [ Common Table Expression ] or { CTE } is a tool for obtaining such temporary result sets that exist within the execution of a given query.

Suppose you wanted to see how many times women's salary in this company rose above the average. You could easily find the average as a value with the query below:
```mysql
SELECT AVG(salary) AS avg_salary
FROM salaries;
```
*To use this resulting value in future expressions, we could use a Common Table Expression:*
```mysql
WITH cte_name AS (SELECT ... FROM ... )
SELECT ...
FROM cte_name ...;
```
*We can use the CTE in future expressions like Insert, Update, or Delete. We'll use a Select statement.*
```mysql
WITH cte AS 
	(SELECT AVG(salary) AS avg_salary FROM salaries)
SELECT SUM(CASE 
	WHEN s.salary > c.avg_salary THEN 1 ELSE 0 END) as no_f_salaries_above_avg,
	COUNT(s.salary) AS total_no_of_salary_contracts
FROM
	salaries s
		JOIN
	employees e ON s.emp_no = e.emp_no AND e.gender = 'F'
		CROSS JOIN
	cte c;
```

""Considering the salary contracts signed by male employees in the company, how many have been signed for a value above the average? Store the output in a column named no_m_salaries_above_avg. In a second column named no_of_m_salary_contracts, provide the total number of contracts signed by men. Use the salary column from the salaries table and the gender column from the employees table. Match the two tables on the employee number column (emp_no).""
```mysql
WITH cte AS 
	(SELECT AVG(salary) AS avg_salary FROM salaries)
SELECT SUM(CASE 
	WHEN s.salary >= c.avg_salary THEN 1 ELSE 0 END) as no_m_salaries_above_avg,
	COUNT(s.salary) AS no_of_m_salary_contracts
FROM
	salaries s
		JOIN
	employees e ON s.emp_no = e.emp_no AND e.gender = 'M'
		JOIN
	cte c;
```


How many female employees' highest contract salary values were higher than the all time company salary average { across all genders }?

Sub-clause 1 is for the CTE to compute the all time average
Sub-clause 2 is for a list of all the highest contract salary values of all female employees
	compare the two, and count values where the female average is higher

The initial average computation:
```mysql
SELECT AVG(salary) AS av_salary
FROM salaries;
```

Then, a select statement to contain all the highest salary contract values of all female employees
```mysql
SELECT s.emp_no, MAX(s.salary) AS highest_salary
FROM salaries S
	JOIN employees e
		ON s.emp_no = e.emp_no
WHERE e.gender = 'F'
GROUP BY e.emp_no;
```

Combined:
```mysql
WITH cte1 AS
(SELECT AVG(salary) AS avg_salary
FROM salaries
),
cte2 AS 
(SELECT s.emp_no, MAX(s.salary) AS f_highest_salary
FROM salaries S
	JOIN employees e
		ON s.emp_no = e.emp_no
WHERE e.gender = 'F'
GROUP BY s.emp_no
)
SELECT 
SUM(CASE WHEN c2.f_highest_salary > c1.avg_salary THEN 1 ELSE 0 END) AS f_highest_salaries_above_avg,
COUNT(e.emp_no) AS females_in_comp
FROM employees e
JOIN cte2 c2 ON c2.emp_no = e.emp_no
JOIN cte1 c1; # why isn't this join defined?
```
*The second Join defined here with cte1 c1 is a Cross Join, as no On was specified. This is OK here because the CTE returns a single row with the average.*
```mysql
WITH cte1 AS
(SELECT AVG(salary) AS avg_salary
FROM salaries
),
cte2 AS 
(SELECT s.emp_no, MAX(s.salary) AS f_highest_salary
FROM salaries S
	JOIN employees e
		ON s.emp_no = e.emp_no
WHERE e.gender = 'F'
GROUP BY s.emp_no
)
SELECT 
COUNT(CASE WHEN c2.f_highest_salary > c1.avg_salary ELSE NULL END) AS f_highest_salaries_above_avg,
COUNT(e.emp_no) AS females_in_comp
FROM employees e
JOIN cte2 c2 ON c2.emp_no = e.emp_no
JOIN cte1 c1; # why isn't this join defined?
```
*Could also be written as:
```mysql
WITH cte1 AS
(SELECT AVG(salary) AS avg_salary
FROM salaries
),
cte2 AS 
(SELECT s.emp_no, MAX(s.salary) AS f_highest_salary
FROM salaries S
	JOIN employees e
		ON s.emp_no = e.emp_no
WHERE e.gender = 'F'
GROUP BY s.emp_no
)
SELECT 
COUNT(CASE WHEN c2.f_highest_salary > c1.avg_salary THEN c2.f_highest_salary ELSE NULL END) AS f_highest_salaries_above_avg,
COUNT(e.emp_no) AS females_in_comp
FROM employees e
JOIN cte2 c2 ON c2.emp_no = e.emp_no
JOIN cte1 c1; # why isn't this join defined?
```
*And with the average calculated:*
```mysql
WITH cte1 AS
(SELECT AVG(salary) AS avg_salary
FROM salaries
),
cte2 AS 
(SELECT s.emp_no, MAX(s.salary) AS f_highest_salary
FROM salaries S
	JOIN employees e
		ON s.emp_no = e.emp_no
WHERE e.gender = 'F'
GROUP BY s.emp_no
)
SELECT 
COUNT(CASE WHEN c2.f_highest_salary > c1.avg_salary THEN c2.f_highest_salary ELSE NULL END) AS f_highest_salaries_above_avg,
COUNT(e.emp_no) AS females_in_comp,
(SUM(CASE WHEN c2.f_highest_salary > c1.avg_salary THEN 1 ELSE 0 END) / COUNT(e.emp_no))*100
FROM employees e
JOIN cte2 c2 ON c2.emp_no = e.emp_no
JOIN cte1 c1; # why isn't this join defined?
```
*We could also round add a symbol to our result:*
```mysql
WITH cte1 AS
(SELECT AVG(salary) AS avg_salary
FROM salaries
),
cte2 AS 
(SELECT s.emp_no, MAX(s.salary) AS f_highest_salary
FROM salaries S
	JOIN employees e
		ON s.emp_no = e.emp_no
WHERE e.gender = 'F'
GROUP BY s.emp_no
)
SELECT 
COUNT(CASE 
	WHEN c2.f_highest_salary > c1.avg_salary THEN c2.f_highest_salary ELSE NULL END
	) AS f_highest_salaries_above_avg,
COUNT(e.emp_no) 
	AS females_in_comp,
CONCAT(ROUND((SUM(CASE WHEN c2.f_highest_salary > c1.avg_salary THEN 1 ELSE 0 END) / COUNT(e.emp_no))*100, 2), '%') 
	AS '% percentage'
FROM 
	employees e
JOIN 
	cte2 c2 ON c2.emp_no = e.emp_no
JOIN 
	cte1 c1; # why isn't this join defined?
```
*The video showed there was no effect on output when the ON c2.emp_no = e.emp_no portion of the join can be commented out. This crashed my MySQL server, however., when executing the query.*

""Considering the salary contracts signed by female employees in the company, how many have been signed for a value below the average? Store the output in a column named no_f_salaries_below_avg. In a second column named total_no_of_salary_contracts, provide the total number of contracts signed by all employees in the company. Use the salary column from the salaries table and the gender column from the employees table. Match the two tables on the employee number column (emp_no).""
```mysql
WITH cte AS 
	(SELECT AVG(salary) AS avg_salary FROM salaries)
SELECT SUM(CASE 
	WHEN s.salary <= c.avg_salary AND e.gender = 'F' THEN 1 ELSE 0 END) as no_f_salaries_below_avg,
	COUNT(s.salary) AS total_no_of_salary_contracts
FROM
	salaries s
		JOIN
	employees e ON s.emp_no = e.emp_no
		JOIN
	cte c;
```