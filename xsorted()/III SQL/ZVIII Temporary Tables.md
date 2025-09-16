Temporary tables can be made to hold result sets frequently searched for. They are only available in the same session as they were created but otherwise behave as standard tables. They can be dropped and called by their title, but if the session is closed, they cease to exist. After a session is closed in which a Temporary Table was created, said table will be immediately lost.

""Obtain a list containing the highest contract salary values signed by all female employees who have worked in the company.""
```mysql
SELECT s.emp_no, MAX(s.salary) AS f_highest_salary
FROM salaries s
JOIN employees e
	ON e.emp_no = s.emp_no 
WHERE gender = 'F'
GROUP BY s.emp_no;
```
*Instead of Joining these two tables every time we need this information, we can create a temporary table with this data to refer to. This is faster and less computationally expensive than recreating it every time it is needed.*
```mysql
CREATE TEMPORARY TABLE temp_table_name
SELECT 
	...,
FROM 
	...;
```

```mysql
CREATE TEMPORARY TABLE f_highest_salaries
SELECT s.emp_no, MAX(s.salary) AS f_highest_salary
FROM salaries s
JOIN employees e
	ON e.emp_no = s.emp_no 
WHERE e.gender = 'F'
GROUP BY s.emp_no;
```
*Then see what it contains:*
```mysql
SELECT * FROM f_highest_salaries;
```
*Find only the emp_no's above 10010:*
```mysql
SELECT * FROM f_highest_salaries
WHERE emp_no > '10010';
```
*And drop the temporary table:*
```mysql
DROP TABLE IF EXISTS f_highest_salaries
```

Temporary tables cannot be invoked more than once. It is locked for use after creation. It cannot be used with self-joins or Unions or Unions All.

Instead of making another temporary table, we could make a CTE:
```mysql
CREATE TEMPORARY TABLE f_highest_salaries
SELECT s.emp_no, MAX(s.salary) AS f_highest_salary
FROM salaries s
JOIN employees e
	ON e.emp_no = s.emp_no 
WHERE e.gender = 'F'
GROUP BY s.emp_no
LIMIT 10;
```
*Like with a Common Table Expression:*
```mysql
WITH cte AS (SELECT 
			s.emp_no, MAX(s.salary) AS f_highest_salary
			FROM salaries s
			JOIN employees e
				ON e.emp_no = s.emp_no 
			WHERE e.gender = 'F'
			GROUP BY s.emp_no
			LIMIT 10
			)
SELECT * FROM f_highest_salaries f1 JOIN cte c;
```
*Or a Union:*
```mysql
WITH cte AS (SELECT 
			s.emp_no, MAX(s.salary) AS f_highest_salary
			FROM salaries s
			JOIN employees e
				ON e.emp_no = s.emp_no 
			WHERE e.gender = 'F'
			GROUP BY s.emp_no
			LIMIT 10
			)
SELECT * FROM f_highest_salaries f1 UNION ALL SELECT * FROM cte c;
```


""Create a temporary table called 'dates' which contains the following three DATETIME values:
	The current date and time
	A month earlier than the current date and time
	A year later than the current date and time""
```mysql
CREATE TEMPORARY TABLE dates
SELECT
	NOW() AS current_date_and_time,
	DATE_SUB(NOW(), INTERVAL 1 MONTH) AS a_month_earlier,
	DATE_SUB(NOW(), INTERVAL -1 YEAR) AS a_year_later;
```
*Date_Sub(date, Interval expr. unit) takes the given date and subtracts the given Interval Expression Unit from said date. In this case, Date_Sub takes the date generated from Now() and subtracts one month from it. Then, the next statement subtracts negative one year, or adds one year to the current date.*
```mysql
SELECT * FROM dates d1
UNION SELECT * FROM dates d2;
```
*Self-Joins with temporary tables is illegal, so the above will return an error. Instead, we can use the CTE workaround demonstrated previously. We make the body of the temporary table's Create query into a sub-clause of the with statement in a Common Table Expression, and then a Self-Join is possible.*
```mysql
SELECT
	NOW() AS current_date_and_time,
	DATE_SUB(NOW(), INTERVAL 1 MONTH) AS a_month_earlier,
	DATE_SUB(NOW(), INTERVAL -1 YEAR) AS a_year_later
```

```mysql
WITH cte AS(
			SELECT
			NOW() AS current_date_and_time,
			DATE_SUB(NOW(), INTERVAL 1 MONTH) AS a_month_earlier,
			DATE_SUB(NOW(), INTERVAL -1 YEAR) AS a_year_later
			)
SELECT * FROM dates d1 JOIN cte c;
```
*Could also use a Union All operator:*
```mysql
WITH cte AS(
			SELECT
			NOW() AS current_date_and_time,
			DATE_SUB(NOW(), INTERVAL 1 MONTH) AS a_month_earlier,
			DATE_SUB(NOW(), INTERVAL -1 YEAR) AS a_year_later
			)
SELECT * FROM dates d1 UNION ALL SELECT * FROM cte c;
```
*The Union stacks the results while the Join strung them together.*

""Execute the following two queries.
1. Create a temporary table called salaries_adjusted_for_inflation based on the data in the salaries table. It should contain the following five fields for all employees:
   1.1   Employee number (emp_no)  
   1.2  Salary value (salary)  
   1.3  A field named inflation_adjusted_salary containing the salary value (salary) rounded to the nearest cent, which should be:  
              - Multiplied by 6.5 if the contract start date (from_date) was between January 1, 1970, and December 31, 1989, inclusive;   
              - Multiplied by 2.8 if the contract start date (from_date) was between January 1, 1990, and December 31, 1999, inclusive;  
              - Multiplied by 3 for the rest of the contracts.  
   1.4   The contract start date (from_date)  
   1.5   The contract end date (to_date).
2. Select all the data from the temporary table just created.""
*Now, the site says my syntax is incorrect somewhere relating to one of the Select statements, however, MySQL does not share this opinion, so I am disregarding this assessment of my code.*
```mysql
CREATE TEMPORARY TABLE salaries_adjusted_for_inflation
SELECT
    s.emp_no, 
    s.salary,
    ROUND((CASE WHEN s.from_date BETWEEN '1970-01-01' AND '1989-12-31' THEN s.salary * 6.5
    WHEN s.from_date BETWEEN '1990-01-01' AND '1999-12-31' THEN s.salary * 2.8
    ELSE s.salary * 3 END),2) AS inflation_adjusted_salary,
    s.from_date,
    s.to_date
FROM salaries s;

SELECT * FROM salaries_adjusted_for_inflation;
```

""Copy the Select statement creating the salaries_adjusted_for_inflation temporary table in the With clause of a Common Table Expression whose top-level Select statement joins the common table expression data with the data from the salaries_adjusted_for_inflation table on the employee number (emp_no).""
```mysql
CREATE TEMPORARY TABLE salaries_adjusted_for_inflation AS
SELECT  emp_no,
        salary,
        CASE
            WHEN from_date BETWEEN '1970-01-01' AND '1989-12-31' THEN ROUND(salary * 6.5, 2)
            WHEN from_date BETWEEN '1990-01-01' AND '1999-12-31' THEN ROUND(salary * 2.8, 2)
            ELSE ROUND(salary * 3, 2)
        END AS inflation_adjusted_salary,
        from_date,
        to_date
    FROM 
        salaries s;


WITH cte AS (SELECT  emp_no,
        salary,
        CASE
            WHEN from_date BETWEEN '1970-01-01' AND '1989-12-31' THEN ROUND(salary * 6.5, 2)
            WHEN from_date BETWEEN '1990-01-01' AND '1999-12-31' THEN ROUND(salary * 2.8, 2)
            ELSE ROUND(salary * 3, 2)
        END AS inflation_adjusted_salary,
        from_date,
        to_date
        FROM salaries)
SELECT * FROM salaries_adjusted_for_inflation s JOIN cte c ON s.emp_no = c.emp_no;
```