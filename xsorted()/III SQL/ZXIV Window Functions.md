Performs a calculation for every row or record of a given database, using other records as a window, or set of rows for the function to be applied. 'Every row' translates to the given row of the iterable loop as it progresses through the specified records. Similar to Aggregate functions.

Aggregate Window Functions { aggregate functions used in the context of widow functions}, and Non-Aggregate Window Functions, which are comprised of Ranking Window Functions and Value Window Functions.

Ranking Window Functions | Row Number()

```mysql
SELECT ..., ROW NUMBER () OVER () AS . . .
FROM ...;
```
*The contents of the parenthesis relates to the window over which the function evaluation will occur. This is an empty window clause until we fill the parenthesis.*
	*Row_Number ( ) will perform the relevant evaluations on **all** query rows with empty parenthesis.*
```mysql
SELECT 
	emp_no, 
	salary, 
	ROW_NUMBER () OVER () AS row_num
FROM 
	salaries;
```
*This query above returned the row_num in the consecutive column for every record pulled from Salaries.*
```mysql
SELECT 
	emp_no, 
	salary, 
	ROW_NUMBER () OVER (PARTITION BY emp_no) AS row_num
FROM 
	salaries;
```
*Including Partition By introduces a function that organizes, or partitions, similarly to the Group By clause. However, Partition By does not modify the underlying data or table, unlike Group By.*
	*For the query above, the return was the same third column but each emp_no had its own incrementing partition. For every emp_no in the columns on the right, the Row_Number rose by one until a new emp_no appeared and the partition and Row_Number reset.*
		*With an empty Partition-By clause, the optimizer will default to a partition of one, where every record is its own partition and the last value of the Row_Number column will be the number of records from the Select statement.*
```mysql
SELECT 
	emp_no, 
	salary, 
	ROW_NUMBER () OVER (PARTITION BY emp_no ORDER BY salary DESC) AS row_num
FROM 
	salaries;
```
*This way, we can have every partition be ordered by the value of their salary in decreasing order. If we wanted to sort the un-partitioned values, we could do so in the same way:*
```mysql
SELECT 
	emp_no, 
	salary, 
	ROW_NUMBER () OVER (ORDER BY salary DESC) AS row_num
FROM 
	salaries;
```

""Retrieve everything stored in the employee number (emp_no), first name (first_name), and last name (last_name) columns from the employees table. Add a fourth column named row_num, which partitions the data by last name, sorts it by employee number in ascending order, and assigns a row number starting from 1 and incrementing for each row in every partition.""
```mysql
SELECT emp_no, first_name, last_name,
ROW_NUMBER () OVER (PARTITION BY last_name ORDER BY emp_no ASC) AS row_num
FROM employees
```

Several Window Functions at Once
```mysql
SELECT 
	emp_no, 
	salary, 
	ROW_NUMBER () OVER () AS row_1,
	ROW_NUMBER () OVER (Partition By emp_no) AS row_2,
	ROW_NUMBER () OVER (Partition By emp_no ORDER BY salary DESC) AS row_3,
	ROW_NUMBER () OVER (ORDER BY salary DESC) AS row_4
FROM 
	salaries;
```
*This output is fairly messy and difficult to interpret. We could add Group By and Order By clauses after the Window Functions to try to reorder the data, or we could abide by the recommendation to only use Window Specifications requiring identical partitions. In this case, Window Functions for rows 2 & 3 and rows 1 & 4 use identical partitions, so these pairs should be used together, not all together as one.*
```mysql
SELECT 
	emp_no, 
	salary, 
	#ROW_NUMBER () OVER () AS row_1,
	ROW_NUMBER () OVER (Partition By emp_no) AS row_2,
	ROW_NUMBER () OVER (Partition By emp_no ORDER BY salary DESC) AS row_3
	#ROW_NUMBER () OVER (ORDER BY salary DESC) AS row_4
FROM 
	salaries;
```
*With identical partitions, we have no need for an exterior Group By or Order By clause.*

""Retrieve the employee number (emp_no) and job title (title) from the titles table, and the salary (salary) from the salaries table. Add a column to the left, named row_num1, starting from 1 incrementing by 1 for each row from the obtained result. Also, add a fifth column, named row_num2, which provides a row position for each record per employee, starting from the total number of records obtained for that employee and continuing down to 1. Include only data about _'Staff'_ members and employees with a number no greater than 10006. Order the result by employee number (emp_no), salary, and row_num1 in ascending order.""
```mysql
SELECT
    ROW_NUMBER () OVER () AS row_num1,
    t.emp_no, 
    t.title, 
    s.salary,
    ROW_NUMBER () OVER (PARTITION BY t.emp_no ORDER BY s.salary DESC) AS row_num2
FROM titles t 
JOIN salaries s ON t.emp_no = s.emp_no
WHERE t.emp_no <= '10006' AND t.title = 'Staff'
ORDER BY t.emp_no, s.salary, row_num1;
```

""Retrieve the employee number (emp_no) and job title (title) from the titles table, and the salary (salary) from the salaries table. Add a fourth column, named row_num1, containing starting from 1 incrementing by 1 for each row for every employee from the obtained result. Also, add a fifth column, named row_num2, which provides the opposite values - starting from the total number of records obtained for a given employee and continuing down to 1. Include only data about _'Staff'_ members and employees with a number no greater than 10006. Order the result by employee number (emp_no), salary, and row_num1 in ascending order.""
```mysql
SELECT t.emp_no, t.title, s.salary,
    ROW_NUMBER () OVER (PARTITION BY t.emp_no ORDER BY s.salary) AS row_num1,
    ROW_NUMBER () OVER (PARTITION BY t.emp_no ORDER BY s.salary DESC) AS row_num2
FROM titles t
JOIN salaries s ON t.emp_no = s.emp_no
WHERE t.title = 'Staff' AND t.emp_no <= '10006'
ORDER BY t.emp_no, s.salary, row_num1;
```
*Technically, this works and provides the requested output from the database without row_num1's Order By clause, but it is better practice to specify the organization rather than to rely on default behavior.*

Alternative Syntax
We can give the window function a *Local* alias to move the clause in our query.

```mysql
SELECT ...,
	ROW_NUMBER () OVER alias AS ...
FROM ...
WINDOW alias ();
```

```mysql
SELECT emp_no, salary,
	ROW_NUMBER () OVER (PARTITION BY emp_no ORDER BY salary DESC) AS row_num
FROM
	salaries;
```
*Can be re-written as:*
```mysql
SELECT emp_no, salary,
	ROW_NUMBER OVER w AS row_num
FROM salaries
WINDOW w AS (PARTITION BY emp_no ORDER BY salary DESC);
```
*Here, the window function is given the alias ' w ' for the function, in which the Over's clause can be contained and referenced. The alternate syntax and original are identical functionally.*


Partition vs. Group By Clauses
Simply put, Group By reduces the number of records returned. Partition By does not effect the number of records returned.

*Partition by can also only be used within the context of applying window functions. For example, when finding salary values, Group By could not be used for the following searches into the database:*
```mysql
SELECT a.emp_no,
		a.salary AS max_salary FROM (
			SELECT emp_no, salary, 
				ROW_NUMBER () OVER w AS row_num
			FROM 
				salaries
			WINDOW w AS (PARTITION BY emp_no ORDER BY salary DESC)) AS a
WHERE a.row_num = 1;
```
*This query takes the salaries and emp_no's from the Salaries table and Partitions by the emp_no with descending order of salary within each partition. This way, we can add a Where clause looking for the first row of every partition: their highest salary. Intuitively, we could change this row to 2 or 3 and obtain a table of their second or third highest salaries respectively.*
```mysql
SELECT a.emp_no,
		a.salary AS max_salary FROM (
			SELECT emp_no, salary, 
				ROW_NUMBER () OVER w AS row_num
			FROM 
				salaries
			WINDOW w AS (PARTITION BY emp_no ORDER BY salary DESC)) AS a
WHERE a.row_num = 2;
```
*With the Partitions By emp_no and Ordered By salary, changing the row_num of the Where clause makes the query return the second row of every partition from the Select statement.*


""Retrieve the employee number (`emp_no`) and the highest contract salary value (`salary`, using the alias `max_salary`) for all managers.
_To obtain the desired output, modify the following query, which finds the department managers' lowest salaries._""
```mysql
SELECT a.emp_no, 
	a.salary AS max_salary FROM (
	SELECT 
		s.emp_no, salary, ROW_NUMBER() OVER w AS row_num
	FROM
		dept_manager dm
	JOIN 
	    salaries s ON s.emp_no = dm.emp_no
	WINDOW w AS (PARTITION BY s.emp_no ORDER BY salary)) a
WHERE a.row_num=1;
```
*Solution:*
```mysql
SELECT a.emp_no, 
	a.salary AS max_salary FROM (
	SELECT 
		s.emp_no, salary, ROW_NUMBER() OVER w AS row_num
	FROM
		dept_manager dm
	JOIN 
	    salaries s ON s.emp_no = dm.emp_no
	WINDOW w AS (PARTITION BY s.emp_no ORDER BY salary DESC)) a
WHERE a.row_num=1;
```


""Retrieve the employee number (`emp_no`) and the third-highest contract salary value (`salary`, using the alias `third_max_salary`) for all managers. To solve the exercise, you need to refer to the_ `_dept_manager_` _and_ `_salaries_` _tables._"" { I don't get this one incredibly well because why did they use ' FROM dept_manager dm ' inside the FROM ( SELECT ... statement? Especially because here ' FROM salaries s ' is used }
```mysql
SELECT a.emp_no, a.salary AS third_max_salary
    FROM (SELECT
            s.emp_no, s.salary, 
            ROW_NUMBER () OVER w AS third_max_salary
        FROM salaries s
        JOIN dept_manager dm ON s.emp_no = dm.emp_no
        WINDOW w AS (PARTITION BY s.emp_no ORDER BY salary DESC)
        ) AS a
WHERE a.third_max_salary = 3;
```
*In their solution they use ' FROM dept_manager dm ' inside the FROM ( SELECT ... statement, so I guess their interchangeable here?*
```mysql
1. SELECT a.emp_no,
2. a.salary as third_max_salary FROM (
3. SELECT
4. s.emp_no, salary, ROW_NUMBER() OVER w AS row_num
5. FROM
6. dept_manager dm
7. JOIN
8. salaries s ON s.emp_no = dm.emp_no
9. WINDOW w AS (PARTITION BY s.emp_no ORDER BY salary DESC)) a
10. WHERE a.row_num = 3;
```


RANK ( ) and DENSE_RANK ( ) 

Function walkthrough:
```mysql
SELECT emp_no, salary, ROW_NUMBER () OVER w AS row_num
FROM salaries
WINDOW w AS (PARTITION BY emp_no ORDER BY salary DESC);
```
*Here we have the classic partition by emp_no & order by salary Window Function. Let's look at one employee closer:*
```mysql
SELECT emp_no, salary, ROW_NUMBER () OVER w AS row_num
FROM salaries
WHERE emp_no = '10001'
WINDOW w AS (PARTITION BY emp_no ORDER BY salary DESC);
```
*It looks like all of their salaries have been unique Integers, but let's let MySQL check for us:*
```mysql
SELECT DISTINCT emp_no, salary, ROW_NUMBER () OVER w AS row_num
FROM salaries
WINDOW w AS (PARTITION BY emp_no ORDER BY salary DESC)
WHERE emp_no = '10001';
```
*The same 17 rows were returned again, so we can assume every salary value for emp_no 10001 is an unique Integer. What if the values were not distinct? What if a manager worked in two departments at different times, and received the same salary for both positions? Essentially, what if an employee signed multiple distinct contracts of the same value over separate time periods?
	We could check with a Count:*
```mysql
SELECT emp_no, (COUNT(salary) - COUNT(DISTINCT salary)) AS diff
FROM salaries
GROUP BY emp_no
HAVING diff > 0
ORDER BY emp_no;
```
*205 rows returned, so we have 205 instances of duplicate values of salaries within a given employees career at this company. Let's take a closer look at one employee; emp_no 11839. Let's check him out with the classics:*
```mysql
SELECT emp_no, salary, ROW_NUMBER () OVER w AS row_num
FROM salaries
WHERE emp_no = '11839'
WINDOW w AS (PARTITION BY emp_no ORDER BY salary DESC);
```
*We see 12 rows, 3 rows containing emp_no which remains 11839, salary which is sorted in Descending order, and row_num, the Window Function counting rows from 1 to 12 starting with 1. Looking closer, the salaries from row_num's 3 to 4 are identical. Guess who can help.*
```mysql
SELECT emp_no, salary, RANK () OVER w AS rank_num
FROM salaries
WHERE emp_no = '11839'
WINDOW w AS (PARTITION BY emp_no ORDER BY salary DESC);
```
*With Rank in replace of Row_Number, we see a similar output. The behavior is similar as it counts the rows in order, resulting in the same final rank_num being 12, with the only difference being the third and fourth positions. They are both rank_num 3; Rank considers every element of the given partition individually. The third and fourth values of the salaries are ranked equally as they were the same, but they are independent of each other in the Rank.
		The only values changed from the Row_Number Function were the fourth value of the third column and said column's name. If we wanted to see the values sequentially considered as if the third and fourth salaries were one position instead of two, Dense_Rank would be used.*
```mysql
SELECT emp_no, salary, DENSE_RANK () OVER w AS rank_num
FROM salaries
WHERE emp_no = '11839'
WINDOW w AS (PARTITION BY emp_no ORDER BY salary DESC);
```
*This time, the third and fourth positions of rank_num are still 3, but the fifth position of the list is 4. Consequently, the final value of this column is 11 instead of the previous 12 as Dense_Rank considers values of the Rank to be one element. Bada-Bing, Bada-Boom.*

In summary, the Rank and Dense_Rank Window Functions must be used with the Order By clause. The rank values are always assigned sequentially and the first value is always equal to the integer one. The subsequent values grow *incrementally by* one, unless there is a duplicate record or value.


""Order and number all contract salary values of employee 10002 from highest to lowest. Store the row numbers in a third column named order_num which assigns different row numbers to identical salary values.
To obtain the desired values, refer to the employee number (emp_no) and salary (salary) columns from the salaries table.""
```mysql
SELECT emp_no, salary, 
    ROW_NUMBER () OVER (PARTITION BY emp_no ORDER BY salary DESC) AS order_num
FROM salaries
WHERE emp_no = '10002';
```

""Order and rank all contract salary values of employee 10002 from highest to lowest. Store the row numbers in a third column named `order_num`. Assign the same rank to identical salary values allowing gaps in the obtained ranks for subsequent rows.

_To obtain the desired values, refer to the employee number (_`_emp_no_`_) and salary (_`_salary_`_) columns from the_ `_salaries_`_table._""
```mysql
SELECT emp_no, salary, 
    RANK () OVER (PARTITION BY emp_no ORDER BY salary DESC) AS order_num
FROM salaries
WHERE emp_no = '10002';
```


""Order and rank all contract salary values of employee 10002 from highest to lowest. Store the row numbers in a third column named `order_num`. Assign the same rank to identical salary values _without_ allowing gaps in the obtained ranks for subsequent rows.

_To obtain the desired values, refer to the employee number (_`_emp_no_`_) and salary (_`_salary_`_) columns from the_ `_salaries_`_table._""
```mysql
SELECT emp_no, salary, 
    DENSE_RANK () OVER (PARTITION BY emp_no ORDER BY salary DESC) AS order_num
FROM salaries
WHERE emp_no = '10002';
```


""Create a query that will complete all the following subtasks at once:
	Obtain data only about managers from the employees database
	Partition the relevant information by departments the managers have worked in
	Arrange the partitions by manger's salary contract values in descending order
	Rank the managers according to their salaries in certain departments ( where you prefer to not lose track of the number of salary contracts signed within each department )
	Display the start and end dates of each salary contract ( call the relevant fields salary_from_date and salary_to_date, respectively )
	Display the first and last date in which an employee has been a manager, according to the data provided in the dept_manager table ( call the relevant fields dept_manager_from_date and dept_maanager_to_date, respectively. )

*It is a complicated query, but we only need data stored on Dept_manager, Departments, and Salaries. Let's build off of the From statement:*
```mysql
FROM 
	dept_manager dm
		JOIN
	salaries s ON dm.emp_no = s.emp_no
		JOIN
	departments d ON dm.dept_no = d.dept_no
WINDOW w AS (PARTITION BY dm.dept_no ORDER BY s.salary DESC)
```
*We'll join these three tables; Dept_manager & Salaries through emp_no, and dept_no for Dept_manager to Departments. Then, we define a Window Function w which partitions the data by dept_no and orders it by salary values in descending order. This is done to satisfy the 'Partition the relevant information by departments the managers have worked in', 'Arrange the partitions by manger's salary contract values in descending order', and 'Rank the managers according to their salaries in certain departments' requirements. Finally, Joining over Dept_manager with Salaries over the emp_no ensures that only managers will be returned.*
```mysql
SELECT
	d.dept_no, 
	d.dept_name, 
	dm.emp_no, 
	RANK () OVER w AS dept_salary_ranking,
	s.salary,
	s.from_date AS salary_from_date,
	s.to_date AS salary_to_date,
	dm.from_date AS dept_manager_from_date,
	dm.to_date AS dept_manager_to_date
FROM 
	dept_manager dm
		JOIN
	salaries s ON dm.emp_no = s.emp_no
			AND 
				s.from_date BETWEEN dm.from_date AND dm.to_date
			AND 
				s.to_date BETWEEN dm.from_date AND dm.to_date
		JOIN
	departments d ON dm.dept_no = d.dept_no
WINDOW w AS (PARTITION BY dm.dept_no ORDER BY s.salary DESC);
```
*We made the select statement last so we could pick the order and aliases of our selections carefully; first, from Departments, we pull the dept_no and dept_name, then the emp_no from Dept_manager. Next, the dept_salary_ranking Rank Window Function is called, then the Salaries' salary, from_date, and to_date. Finally, the Dept_manager's from_date's and to_date's are called with their respective aliases. Additionally, the Salaries' to and from _dates are restricted to be between the Dept_manager's to and from _dates for a given employee. This restriction changes the misleading output from 405 rows to the correct output with 149 rows.*


""Allowing gaps in the obtained ranks for subsequent rows, rank the contract salary values from highest to lowest for employees 10001, 10002, 10003, 10004, 10005, and 10006. 

Every row in the desired output should contain an employee number (`emp_no`) obtained from the `employees` table, and a `salary` value obtained from the `salaries` table. Additionally, include the salary ranking values between the two columns in a field named `employee_salary_ranking`.""
```mysql
SELECT 
    e.emp_no, 
    RANK () OVER w AS employee_salary_ranking,
    s.salary
FROM employees e 
JOIN salaries s ON e.emp_no = s.emp_no
    AND e.emp_no IN ('10001', '10002', '10003', '10004', '10005', '10006')
WINDOW w AS (PARTITION BY e.emp_no ORDER BY s.salary DESC);
```

""Without allowing gaps in the obtained ranks for subsequent rows, rank the contract salary values from highest to lowest for employees 10001, 10002, and 10003. 

Every row in the desired output should contain the relevant employee number (`emp_no`) and the hire date (`hire_date`) from the `employees` table, as well as the relevant `salary`value and the start date (`from_date`) from the `salaries`table. Additionally, include the salary ranking values in a field named `employee_salary_ranking`.

Retrieve only data for contracts that have started prior to 2000. Sort your data by the  `emp_no` in ascending order, referring to the `employees` table.""
```mysql
SELECT 
    e.emp_no, 
    DENSE_RANK () OVER w AS employee_salary_ranking,
    s.salary,
    e.hire_date,
    s.from_date
FROM employees e 
JOIN salaries s ON e.emp_no = s.emp_no
    AND e.emp_no IN ('10001', '10002', '10003')
WHERE s.from_date < '2000-01-01'
WINDOW w AS (PARTITION BY e.emp_no ORDER BY s.salary DESC)
ORDER BY e.emp_no;
```


Other than Ranking Window Functions, there are also Value Window Functions
As opposed to Ranking, Value Window Functions return a value that can be found in the database.


LAG ( ) and LEAD ( ) 
LAG ( ) returns the value from a specified field of a record that precedes the current row, i.e., the value that lags the current value
LEAD ( ) returns the value from a specified field of a record that procedes the current row, i.e., the value that leads the current value

Now, we want a query that finds the following:
	The salary values from all contracts that the employee 10001 had ever signed while working for the company { ASC order }
	A column showing the previous salary value from our ordered list
	A column showing the next salary value from our ordered list
	A column displaying the difference between the current and previous salary of a given record from the list 
	A column displaying the difference between the next and current salary of a given record from the list
			*This means an emp_no column, a salary column, and four rows whose values are derived from the previous two column's values.*
*We also know that emp_no, salary, from_date, and to_dates, so it is the only table we'll need. Furthermore, we're only looking at emp_no 10001, so we can add a Where clause now:*
```mysql
SELECT emp_no, salary
FROM salaries
WHERE emp_no = '10001
```

Now, to reference a value previously selected in the query, we need the Lag ( ) Window Function. Its syntax, which is similar to Rank's, is below:
```mysql
SELECT ...,
	LAG(column_name_ OVER () AS ...
FROM ...,;
```
*This is the salary column in our case:*
```mysql
SELECT 
	emp_no, 
	salary,
	LAG(salary) OVER l AS previous_salary,
	LEAD(salary) OVER l AS next_salary,
	salary - LAG(salary) OVER l AS diff_salary_current_previous,
	LEAD(salary) OVER l - salary AS diff_salary_consecutive_current
FROM 
	salaries
WHERE 
	emp_no = '10001'
WINDOW l AS (ORDER BY salary);
```

""Retrieve the following data from the `salaries` table:

- employee number (`emp_no`)  
- salary (`salary`)  
- use a window function to obtain the salary value of three contracts prior to the given employee contract salary value, if applicable. Name the column `_before_previous_salary`  
- use a window function to obtain the salary value of three contracts after the given employee contract salary value, if applicable. Name the column `_after_next_salary`.

To obtain the desired output, partition the data by employee number (`emp_no`) and order by salary (`salary`) in ascending order. Retrieve only the first one hundred rows of data.""
```mysql
SELECT 
	emp_no, 
	salary,
	LAG(salary, 3) OVER l AS _before_previous_salary,
	LEAD(salary, 3) OVER l AS _after_next_salary
FROM 
	salaries
WINDOW l AS (PARTITION BY emp_no ORDER BY salary)
LIMIT 100;
```