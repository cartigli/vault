In MySQL, queries and some parts of queries and subprocess produces a temporary dataset, or a result
	A Common Table Expression { CTE } is a tool for obtaining such temporary result sets that exist within the execution of a given query.

Suppose you wanted to see how many times women's salary in this company rose above the average. You could easily find the average as a value with the query below:
```mysql
SELECT AVG(salary) AS avg_salary
FROM salaries;
```

To use this resulting value in future expressions, we could use a Common Table Expression:
```mysql
WITH cte_name AS (SELECT ... FROM ... )
SELECT ...
FROM cte_name ...;
```
*We can use the CTE in future expressions like Insert, Update, or Delete. We'll use a Select statement.*
```mysql
WITH cte AS (SELECT AVG(salary) AS avg_salary FROM salaries)
SELECT SUM(CASE WHEN s.salary > c.avg_salary THEN 1 ELSE 0 END) as no_f_salaries_above_avg,
COUNT(s.salary) AS total_no_of_salary_contracts
FROM
	salaries s
		JOIN
		employees e ON s.emp_no = e.emp_no AND e.gender = 'F'
			CROSS JOIN
		cte c;
```
