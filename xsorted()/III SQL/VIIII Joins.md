\usepackage{tikz}
\usetikzlibrary{positioning, shapes.multipart, arrows.meta}
\usepackage{tikz}

The SQL tool that allows us to construct a relationship between objects.

Joins must be constructed over a column the two tables have in common. It shows a result set, containing fields *derived* from two or more tables.

```
┌─────────────────┐          ┌─────────────────┐
│  employees      ├||──────|<┤  dept_manager   ├>|┐  ┌──────────────────┐
├─────────────────┤          ├─────────────────┤  └||┤   departments    │
│PK mep_no INT    ├||─────┐  │FK dept_no CHAR4 │     ├──────────────────┤
│ birth_date DATE │       │  │FK emp_no INT    │     │PK dept_no CHR4   ├││┐
│ first_name VCHR ├||───┐ │  │ from_date DATE  │     │ dept_name VCHR40 │  │
│ last_name VCHR  │     │ │  │ to_date DATE    │     └──────────────────┘  │
│ gender ENUM     ├||─┐ │ │  └─────────────────┘  ┌────────────────┐       │
│ hire_date DATE  │   │ │ └─────────────────────|<┤   dept_emp     ├>|─────┘
└─────────────────┘   │ │   ┌────────────────┐    ├────────────────┤
  ┌───────────────────┘ └─|<┤     titles     │    │FK emp_no INT   │
  │   ┌────────────────┐    ├────────────────┤    │FK dept_no CHR4 │
  └─|<┤    salaries    │    │FK emp_no INT   │    │ from_date DATE │
      ├────────────────┤    │ title VCHR50   │    │ to_date DATE   │
      │FK emp_no INT   │    │ from_date DATE │    └────────────────┘
      │ salary INT     │    │ to_date DATE   │
      │ from_date DATE │    └────────────────┘
      │ to_date DATE   │
      └────────────────┘
```


INNER JOIN
Below we have both out tables Dept_manager  and Departments shown as circles. Together, they have the dept_no in common,; as an item of the table Dept_manager, and as the Primary Key of the Departments table. Therefore, the Result Set of these two tables is dept_no.

```tikz
\begin{document}
\begin{tikzpicture}
    % Fill the overlap area only
    \begin{scope}
        \clip (-1,0) circle (2.2cm);
        \fill[gray!30] (1,0) circle (2.2cm);
    \end{scope}
    
    % Draw the circle outlines
    \draw (-1,0) circle (2.2cm);
    \draw (1,0) circle (2.2cm);
    
    % Add labels at top
    \node at (-1.75,2.5) {\textbf{Dept-manager}};
    \node at (1.75,2.5) {\textbf{Departments}};
    
    % Text in the overlap - white text on colored background
    \node[align=left, font=\small, text=white] at (0,.5) {
        dept\_no
    };
    
    % List in Departments circle (right)
    \node[align=left, font=\small] at (2.2,0) {
        dept\_no\\
        dept\_name
    };
    
    % List in Dept-manager circle (left)  
    \node[align=left, font=\small] at (-2.2,0) {
        dept\_no\\
        emp\_no\\
        from\_date\\
        to\_date
    };
\end{tikzpicture}
\end{document}
```
*Dept_no is the matching value here, and the rest are considered non-matching records in this case.*

```mysql
SELECT 
	table_1.column_name[s], table_2.column_name[s]
FROM 
	table_1
JOIN 
	table_2 ON table_1.column_name = table_2.column_name;
```
*1. Select all columns you wish to see in the result and the tables they originate from. 2. FROM and JOIN show the tables we are matching. 3 ON relates the columns by quoting them over the equals sign to show SQL where to pull the matching values from.*
*You can also give an alias for the table names without the AS command in this case:*
```mysql
SELECT 
	t1.column_name[s], t2.column_name[s],
FROM 
	table_1 t1
JOIN 
	table_2 t2 ON t1.column_name = t2.column_name;
```
*This way it becomes much easier to spell out the entire relationship.*

Practice with the preconfigured dataset: Retrieve all employee numbers (`emp_no`) and contract start dates (`from_date`) from the department employees table (`dept_emp`). Add a third column, displaying the name of the department they have signed for (`dept_name` from the `departments`table):
```mysql
SELECT 
	de.emp_no, de.from_date, d.dept_name
FROM 
	dept_emp de
JOIN 
	departments d ON de.dept_no = d.dept_no
ORDER BY 
	de.emp_no;
```
*We are making a Join of the two given tables over their common ground; dept_no. We also defined their aliases with From and Inner Join. The columns they are joined over need not be named the same.*
	*In our practice set, the departments table had some Null values in both columns of its contents. Neither of either of these values are considered as only Non-Null matching values are in play. If there is a complete record in one table that is vacant in the other, it will not be shown*
			*If the result set is empty, this simply means their are no relationships between the tables.*

LEFT JOIN
A join of the components of the primary table in the join.
	*It is akin to all the matching values of two tables plus all the values of the primary table that match no values from the secondary values | It is the overlapping region from the inner join in addition to the left outer circle of the diagram.*
```tikz
\begin{document}
\begin{tikzpicture}
    % Fill the left circle first
    \fill[gray!30] (-1,0) circle (2.2cm);
    
    % "Erase" the overlapping part by filling the right circle with white
    \fill[white] (1,0) circle (2.2cm);
    
    % Draw the circle outlines
    \draw (-1,0) circle (2.2cm);
    \draw (1,0) circle (2.2cm);
    
    % Add labels at top
    \node at (-1.75,2.5) {\textbf{Dept-manager}};
    \node at (1.75,2.5) {\textbf{Departments}};
    
    % Text in the overlap - white text since this area is now white background
    \node[align=left, font=\small] at (0,.5) {
        dept\_no
    };
    
    % List in Departments circle (right)
    \node[align=left, font=\small] at (2.2,0) {
        dept\_no\\
        dept\_name
    };
    
    % List in Dept-manager circle (left) - white text on colored background
    \node[align=left, font=\small, text=white] at (-2.2,0) {
        dept\_no\\
        emp\_no\\
        from\_date\\
        to\_date
    };
\end{tikzpicture}
\end{document}
```

```mysql
SELECT 
	q.column_name[s], t.column_name[s],
FROM 
	table_1 q
LEFT JOIN 
	table_2 t ON q.column_name = t.column_name;
```

RIGHT JOIN
The same as a left join but the direction of the comparison is swapped.

```tikz
\begin{document}
\begin{tikzpicture}
    % Fill the right circle first
    \fill[gray!30] (1,0) circle (2.2cm);
    
    % "Erase" the overlapping part by filling the left circle with white
    \fill[white] (-1,0) circle (2.2cm);
    
    % Draw the circle outlines
    \draw (-1,0) circle (2.2cm);
    \draw (1,0) circle (2.2cm);
    
    % Add labels at top
    \node at (-1.75,2.5) {\textbf{Dept-manager}};
    \node at (1.75,2.5) {\textbf{Departments}};
    
    % Text in the overlap - normal black text since this area is white
    \node[align=left, font=\small] at (0,.5) {
        dept\_no
    };
    
    % List in Departments circle (right) - white text on colored background
    \node[align=left, font=\small, text=white] at (2.2,0) {
        dept\_no\\
        dept\_name
    };
    
    % List in Dept-manager circle (left) - normal text since unfilled
    \node[align=left, font=\small] at (-2.2,0) {
        dept\_no\\
        emp\_no\\
        from\_date\\
        to\_date
    };
\end{tikzpicture}
\end{document}
```

```mysql
SELECT 
	q.column_name[s], t.column_name[s],
FROM 
	table_1 q
RIGHT JOIN 
	table_2 t ON q.column_name = t.column_name;
```


The Old Syntax
We have several notes here; initially, right and left joins are identical in function. If the position of both tables is swapped, using a Left Join on the original positioning will return the same result as if they were switched and a Right Join was used.
	Furthermore, the same output as the inner join can be achieved with the outdated syntax which uses Where. This has the same effect and resulting table but is more computationally expensive and so less efficient.

```mysql
SELECT t1.column_name, t1.column_name,..., t2.column_name,...
FROM 
	table_1 t1,
	table_2 t2
WHERE
	t.column_name = t2.column_name;
```

Question:
The new and the old join syntax - Exercise #1
Retrieve a table containing three columns:
1. The employee number (`emp_no`) as recorded in the departments manager table (`dept_manager`).
2. Their contract salary value (`salary`), obtained from the `salaries` table.  
3. The start date of their contracts (`from_date`).
Aim to write your query using the old join syntax.
SOLUTION:
```mysql
SELECT 
    d.emp_no, s.salary, s.from_date
FROM
    dept_manager d,
    salaries s
WHERE
    d.emp_no = s.emp_no;
```


JOIN and WHERE
Join is used to form the connection and where defines the conditions under which the connections are to be made.

Say we want to know the first and last names of every employee who was paid over $145,000 this year. We need emp_no, first_name, and last_name from the Employees table, and salary from Salaries.
```mysql
SELECT e.emp_no, e.first_name, e.last_name, s.salary
FROM employees e
JOIN salaries s ON e.emp_no = s.emp_no
WHERE s.salary > 145000;
```

Retrieve the employee number (`emp_no`), first name (`first_name`), last name (`last_name`), and hire date (`hire_date`) of all `employees` whose last name is _'Bamford'_. Add a fifth column displaying their job title (`title`), as recorded in the `titles` table. Sort your output by employee number in ascending order.
Solution:
```mysql
SELECT e.emp_no, e.first_name, e.last_name, t.title
FROM employees e
JOIN titles t ON e.emp_no = t.emp_no
WHERE first_name = 'Bamford'
ORDER BY e.emp_no ASC;
```


CROSS JOIN
A Cross Join takes the values from a given table and connects them with all the values from the table we want to join it with. This is in contrast to an Inner Join which connects only the matching values. A Cross Join connects all values, not just those that much. This is called the Cartesian product of two sets.$$A :\begin{bmatrix} x \\ y \\ z \end{bmatrix} \text{, B :} \begin{bmatrix} 1 \\ 2 \\ 3 \end{bmatrix}\text{, A x B :} \begin{bmatrix} (x,1) & (x,2) & (x,3) \\ (y,1) & (y,2) & (y,3) \\ (z,1) & (z,2) & (z,3) \end{bmatrix}= \text{Cartesian Product}$$
*This is useful when the two tables are not well connected.*
*Not functionally different from the Inner or Old Syntax Joins.*

REQ:
Return a list with the first two employees (i.e. employees _10001_ and _10002_) with all the departments they can be assigned to. To obtain the desired output, refer to all column from the departments and department employees tables (departments, dept_emp). Order your output by employee number (emp_no) and department name (dept_name).
The order of your field list is as follows:
	Department number (dept_no)
	Department name (dept_name)
	Employee number (emp_no)
	Start date (from_date)
	End date (to_date)
Solution:
```mysql
SELECT d.*, de.*
FROM departments d,
    dept_emp de
WHERE de.emp_no IN (10001, 10002)
ORDER BY de.emp_no, d.dept_name;
```



JOIN w/ AGGREGATEs
Join commands can include Aggregate functions in their query.

For example, finding the average of all the salaries for men and women independently:
```mysql
SELECT e.emp_no, e.gender, AVG(s.salary) AS av_salary
FROM employees e,
JOIN
	salaries s ON e.emp_no = s.emp_no
GROUP BY gender;
```
*However, the above will return an error as e.emp_no is not being grouped despite the fact that it was selected first. To avoid this error, remove e.emp_no from the Selection.*
```mysql
SELECT e.gender, AVG(s.salary) AS av_salary
FROM employees e,
JOIN
	salaries s ON e.emp_no = s.emp_no
GROUP BY gender;
```



JOINING w/ Multiple Tables
Joins can be made over more than two tables, as long as they have values to relate across
<u>employees</u>
```
┌─────────────────┐       ┌─────────────────┐
│  employees      ├||───|<┤  dept_manager   ├>|┐  ┌──────────────────┐
├─────────────────┤       ├─────────────────┤  └||┤   departments    │
│PK mep_no INT    │       │FK dept_no CHAR4 │     ├──────────────────┤
│ birth_date DATE │       │FK emp_no INT    │     │PK dept_no CHR4   │
│ first_name VCHR │       │ from_date DATE  │     │ dept_name VCHR40 │
│ last_name VCHR  │       │ to_date DATE    │     └──────────────────┘
│ gender ENUM     │       └─────────────────┘
│ hire_date DATE  │
└─────────────────┘
```
*Say we needed all the managers' first and last names, their hire date, promotion to manager dates, and their departments. From the Employees table, we can get the first and last names, as well as the hire_date. From Dept_manager, we can find their from_date, and from Departments we can find their dept_name. Employees is connected to Dept_manager through emp_no [ Primary Key to Employees; Foreign Key to Dept_manager ] and Dept_manager is connected to Departments through dept_no [ Primary key to Departments; Foreign Key to Dept_manager ]. Therefore, we should join them as such.*
```mysql
SELECT e.first_name, e.last_name, e.hire_date, dm.from_date, d.dept_name
FROM employees e
JOIN dept_manager dm ON e.emp_no = dm.emp_no
JOIN departments d ON dm.dept_no = d.dept_no
GROUP BY e.first_name;
```

"Retrieve all _Senior Engineers_' first and last name (`first_name`, `last_name`), hire dates (`hire_date`), job titles (`title`), start dates (`from_date`), and names of the departments they are working in (`dept_name`). To obtain the desired result, you should refer to data from the following tables: `employees`, `titles`, `departments`, `dept_emp`."
```mysql
SELECT e.first_name, e.last_name, e.hire_date, t.title, de.from_date, d.dept_name
FROM employees e
JOIN titles t ON e.emp_no = t.emp_no
JOIN dept_emp de ON de.emp_no = e.emp_no
JOIN departments d ON d.dept_no = de.dept_no
WHERE t.title = 'Senior Engineer';
```

"Let's find the names of all departments and determine the average salary paid to each of them."
```
┌─────────────────┐          ┌─────────────────┐
│  employees      ├||──────|<┤  dept_manager   ├>|┐  ┌──────────────────┐
├─────────────────┤          ├─────────────────┤  └||┤   departments    │
│PK mep_no INT    ├||─────┐  │FK dept_no CHAR4 │     ├──────────────────┤
│ birth_date DATE │       │  │FK emp_no INT    │     │PK dept_no CHR4   ├││┐
│ first_name VCHR ├||───┐ │  │ from_date DATE  │     │ dept_name VCHR40 │  │
│ last_name VCHR  │     │ │  │ to_date DATE    │     └──────────────────┘  │
│ gender ENUM     ├||─┐ │ │  └─────────────────┘  ┌────────────────┐       │
│ hire_date DATE  │   │ │ └─────────────────────|<┤   dept_emp     ├>|─────┘
└─────────────────┘   │ │   ┌────────────────┐    ├────────────────┤
  ┌───────────────────┘ └─|<┤     titles     │    │FK emp_no INT   │
  │   ┌────────────────┐    ├────────────────┤    │FK dept_no CHR4 │
  └─|<┤    salaries    │    │FK emp_no INT   │    │ from_date DATE │
      ├────────────────┤    │ title VCHR50   │    │ to_date DATE   │
      │FK emp_no INT   │    │ from_date DATE │    └────────────────┘
      │ salary INT     │    │ to_date DATE   │
      │ from_date DATE │    └────────────────┘
      │ to_date DATE   │
      └────────────────┘
```
These tables are not immediately connected. Salaries hold the salaries information, and departments contains the dept_name's. We could connect Departments to Dept_manager through dept_no, connect Dept_manager to Employees through emp_no, and finally connect Salaries through emp_no, as the previous Join suggests, but this is inefficient. MySQL allows us to 'shortcut' through the emp_no's in Dept_manager and Salaries, shorting the connection created.
```mysql
SELECT d.dept_name, AVG(s.salary)
FROM departments d
JOIN dept_manager dm ON dm.dept_no = d.dept_no
JOIN salaries s ON dm.emp_no = s.emp_no;
```
*Without GROUP BY in this Join, MySQL automatically picks an order and grouping by the first returned dept_name. We need to include this to see the individual dept_name's with their respective average salaries.*
```mysql
SELECT d.dept_name, AVG(s.salary)
FROM departments d
JOIN dept_manager dm ON dm.dept_no = d.dept_no
JOIN salaries s ON dm.emp_no = s.emp_no
GROUP BY d.dept_name;
```
*Although we never explicitly selected dept_no's, we did join over them so we can additionally sort by this field.*
```mysql
SELECT d.dept_name, AVG(s.salary) AS salary
FROM departments d
JOIN dept_manager dm ON dm.dept_no = d.dept_no
JOIN salaries s ON dm.emp_no = s.emp_no
GROUP BY d.dept_name
ORDER BY d.dept_no;
```
*Or, we could order it by the Average salary we found, which is more intuitively meaningful.*
```mysql
SELECT d.dept_name, AVG(s.salary) AS salary
FROM departments d
JOIN dept_manager dm ON dm.dept_no = d.dept_no
JOIN salaries s ON dm.emp_no = s.emp_no
GROUP BY d.dept_name
ORDER BY salary;
```
*Or, we could use the Average salaries' Alias.*
*If we wanted to find only departments in which the average manager makes over x amount, we could use Having which applies a condition to a Group By clause.*
```mysql
SELECT d.dept_name, AVG(s.salary) AS salary
FROM departments d
JOIN dept_manager dm ON dm.dept_no = d.dept_no
JOIN salaries s ON dm.emp_no = s.emp_no
GROUP BY d.dept_name
HAVING salary > 75000
ORDER BY salary;
```

"Calculate the average salary (`salary`), as recorded in the `salaries` table, for each job title (`title`) as listed in the `titles` table, considering all contracts ever signed. Name the second column `avg_salary`and make sure to round the average salary to the nearest cent. Only include records where the average salary is less than $75,000. Sort the results from highest to lowest average salary."
```mysql
SELECT t.title, ROUND(AVG(s.salary),2) AS avg_salary
FROM salaries s
JOIN titles t ON s.emp_no = t.emp_no
GROUP BY t.title
HAVING avg_salary < 75000
ORDER BY avg_salary DESC;
```


UNION | UNION ALL
Used to combine multiple Select statements into a single output.

```mysql
SELECT n columns
FROM table_1
UNION ALL SELECT n columns
FROM table_2
```
*We have to select the same amount columns from each table, they must have the same name, be in the same order, and contain related data types.*
Following the class, he made a duplicate value in for employees, and then added columns containing only Null values to each table so they had the same number and name of columns inside his Union All command. He then showed the same thing run with Union. Does this make any sense for showing this example of the uses and use for Union | Union All?
```mysql
SELECT
	e.emp_no,
	e.first_name,
	e.last_name,
	NULL AS dept_no,
	NULL AS from_date
FROM
	employees_dup e
WHERE
	e.emp_no = 10001
UNION ALL SELECT
	NULL AS emp_no,
	NULL AS first_name,
	NULL AS last_name,
	dm.dept_no,
	dm.from_date
FROM
	dept_manager dm;
```
*Union retrieves only distinct values while Union All retrieves the duplicate records. Additionally, Union's are more resource expensive than Union All.*

"Use UNION to combine data from two subsets in the `employees_10` database. The first subset should contain the employee number (`emp_no`), first name (`first_name`), and last name (`last_name`) of all employees whose family name is _'Bamford'_. The second subset should contain the department number (`dept_no`) and start date (`from_date`) of all managers, as recorded in the departments manager table (`dept_manager`). Ensure to provide null values in all empty columns for each subset."
```mysql
SELECT
    e.emp_no,
    e.first_name,
    e.last_name,
    NULL AS dept_no,
    NULL AS from_date
FROM 
    employees e 
WHERE 
    last_name = 'Bamford'
UNION SELECT 
    NULL AS emp_no,
    NULL AS first_name,
    NULL AS last_name,
    d.dept_no,
    d.from_date
FROM 
    dept_manager d;
```
I don't see the value in Unions because why not use where and select from multiple tables? Or a Join with a Where clause? I am missing some crucial component of Unions, likely about some aspect of their behavior with duplicates.




SUBQUERIES
Inner queries which ran inside of outer queries.

```mysql
SELECT
	t1.column_1, t1.column_2
FROM
	table_1 t1
WHERE
	t1.common_column IN (SELECT
							t2.common_column
						FROM
							table_2 t2);
```

"Use a subquery with an IN operator inside a WHERE clause to obtain the employee number (`emp_no`), department number (`dept_no`), and contract start date (`from_date`) from the `dept_manager` table. Retrieve only data about managers born in or after 1955."
```mysql
SELECT d.emp_no,  d.dept_no, d.from_date
FROM dept_manager d 
WHERE d.emp_no IN (SELECT
                    emp_no
                FROM 
                    employees 
                WHERE 
                    birth_date >= '1955-01-01');
```

"Use a subquery with EXISTS inside a WHERE clause of an outer query to retrieve all data from the `salaries` table. Specify in the subquery that you are only interested in individuals whose job title is _'Engineer'_."
```mysql
SELECT *
FROM salaries s
WHERE EXISTS (SELECT * 
                FROM 
                    titles t 
                WHERE
                    t.emp_no = s.emp_no
                    AND t.title = 'Engineer' 
            );
```



TASK:
Assign employee number 110022 as a manager to all employees from 10001 to 10020, and employee number 110039 as a manager to all employees from 10021 to 10040.

```mysql
SELECT emp_no
FROM dept_manager
WHERE
	emp_no = 110022
```
*Shows us the employ currently under the emp_no: 110022 which is on the dept_manager table. We'll use this as the Inner query of another query. This is the Inner most block of our query.*
```mysql
SELECT 
	e.emp_no AS employee_ID, 
	MIN(de.dept_no) AS department_code,
		(SELECT 
			emp_no
		FROM 
			dept_manager
		WHERE
			emp_no = 110022) AS manager_ID
FROM employees e
JOIN dept_emp de ON e.emp_no = de.emp_no
WHERE e.emp_no <= 10020
GROUP BY e.emp_no
ORDER BY e.emp_no;
```
*We were returned a table containing three rows: employee_ID, department_code, and manager_ID. Employee_ID is emp_no's 10001 - 10020, department_code is the dept_no minimum for each emp_no pulled from the dept_manager table [ to stop duplicates? ], and the manager_ID is 110022 for every record in this table. This is the second Inner most query.*
```mysql
SELECT A.*
FROM
	(SELECT 
		e.emp_no AS employee_ID, 
		MIN(de.dept_no) AS department_code,
			(SELECT 
				emp_no
			FROM 
				dept_manager
			WHERE
				emp_no = 110022) AS manager_ID
	FROM employees e
	JOIN dept_emp de ON e.emp_no = de.emp_no
	WHERE e.emp_no <= 10020
	GROUP BY e.emp_no
	ORDER BY e.emp_no) AS A;
```
*Output is the exact same as above.*
```mysql
SELECT A.*
FROM
	(SELECT 
		e.emp_no AS employee_ID, 
		MIN(de.dept_no) AS department_code,
			(SELECT 
				emp_no
			FROM 
				dept_manager
			WHERE
				emp_no = 110022) AS manager_ID
	FROM employees e
	JOIN dept_emp de ON e.emp_no = de.emp_no
	WHERE e.emp_no <= 10020
	GROUP BY e.emp_no
	ORDER BY e.emp_no) AS A
UNION SELECT
	B.*
FROM
	(SELECT 
		e.emp_no AS employee_ID, 
		MIN(de.dept_no) AS department_code,
			(SELECT 
				emp_no
			FROM 
				dept_manager
			WHERE
				emp_no = 110039) AS manager_ID
	FROM employees e
	JOIN dept_emp de ON e.emp_no = de.emp_no
	WHERE e.emp_no > 10020
	GROUP BY e.emp_no
	ORDER BY e.emp_no
	LIMIT 20) AS B;
```
*Make one more outer function for the function and duplicate it with the modifications for the second group of employees designated to be managed by the second employee. Change the Inner most function looking for the **manager**'s emp_no to be 110039, switch the directional of the greater than operator [ was less than ], and add a Limit of 20 right after the Order By clause. Finally, change the Aliases from A to B.*

Big Boy:
```mysql
SELECT A.*
FROM
	(SELECT 
		e.emp_no AS employee_ID, 
		MIN(de.dept_no) AS department_code,
			(SELECT 
				emp_no
			FROM 
				dept_manager
			WHERE
				emp_no = 110022) AS manager_ID
	FROM employees e
	JOIN dept_emp de ON e.emp_no = de.emp_no
	WHERE e.emp_no <= 10020
	GROUP BY e.emp_no
	ORDER BY e.emp_no) AS A
UNION SELECT
	B.*
FROM
	(SELECT 
		e.emp_no AS employee_ID, 
		MIN(de.dept_no) AS department_code,
			(SELECT 
				emp_no
			FROM 
				dept_manager
			WHERE
				emp_no = 110039) AS manager_ID
	FROM employees e
	JOIN dept_emp de ON e.emp_no = de.emp_no
	WHERE e.emp_no > 10020
	GROUP BY e.emp_no
	ORDER BY e.emp_no
	LIMIT 20) AS B
UNION SELECT
	C.*
FROM
	(SELECT 
		e.emp_no AS employee_ID, 
		MIN(de.dept_no) AS department_code,
			(SELECT 
				emp_no
			FROM 
				dept_manager
			WHERE
				emp_no = 110039) AS manager_ID
	FROM employees e
	JOIN dept_emp de ON e.emp_no = de.emp_no
	WHERE e.emp_no = 10022
	GROUP BY e.emp_no
	ORDER BY e.emp_no) AS C
UNION SELECT
	D.*
FROM
	(SELECT 
		e.emp_no AS employee_ID, 
		MIN(de.dept_no) AS department_code,
			(SELECT 
				emp_no
			FROM 
				dept_manager
			WHERE
				emp_no = 110022) AS manager_ID
	FROM employees e
	JOIN dept_emp de ON e.emp_no = de.emp_no
	WHERE e.emp_no = 10039
	GROUP BY e.emp_no
	ORDER BY e.emp_no) AS U;
```

```mysql
INSERT INTO emp_manager
SELECT U.*
FROM(SELECT A.*
	FROM
		(SELECT 
			e.emp_no AS employee_ID, 
			MIN(de.dept_no) AS department_code,
				(SELECT 
					emp_no
				FROM 
					dept_manager
				WHERE
					emp_no = 110022) AS manager_ID
		FROM employees e
		JOIN dept_emp de ON e.emp_no = de.emp_no
		WHERE e.emp_no <= 10020
		GROUP BY e.emp_no
		ORDER BY e.emp_no) AS A
	UNION SELECT
		B.*
	FROM
		(SELECT 
			e.emp_no AS employee_ID, 
			MIN(de.dept_no) AS department_code,
				(SELECT 
					emp_no
				FROM 
					dept_manager
				WHERE
					emp_no = 110039) AS manager_ID
		FROM employees e
		JOIN dept_emp de ON e.emp_no = de.emp_no
		WHERE e.emp_no > 10020
		GROUP BY e.emp_no
		ORDER BY e.emp_no
		LIMIT 20) AS B
	UNION SELECT
		C.*
	FROM
		(SELECT 
			e.emp_no AS employee_ID, 
			MIN(de.dept_no) AS department_code,
				(SELECT 
					emp_no
				FROM 
					dept_manager
				WHERE
					emp_no = 110039) AS manager_ID
		FROM employees e
		JOIN dept_emp de ON e.emp_no = de.emp_no
		WHERE e.emp_no = 10022
		GROUP BY e.emp_no
		ORDER BY e.emp_no) AS C
	UNION SELECT
		D.*
	FROM
		(SELECT 
			e.emp_no AS employee_ID, 
			MIN(de.dept_no) AS department_code,
				(SELECT 
					emp_no
				FROM 
					dept_manager
				WHERE
					emp_no = 110022) AS manager_ID
		FROM employees e
		JOIN dept_emp de ON e.emp_no = de.emp_no
		WHERE e.emp_no = 10039
		GROUP BY e.emp_no
		ORDER BY e.emp_no) AS U);
```






mine:
```mysql
USE employees;

INSERT INTO emp_manager
SELECT U.*
FROM(SELECT A.*
	FROM
		(SELECT 
			e.emp_no AS employee_ID, 
			MIN(de.dept_no) AS department_code,
				(SELECT 
					emp_no
				FROM 
					dept_manager
				WHERE
					emp_no = 110022) AS manager_ID
		FROM employees e
		JOIN dept_emp de ON e.emp_no = de.emp_no
		WHERE e.emp_no <= 10020
		GROUP BY e.emp_no
		ORDER BY e.emp_no) AS A
	UNION SELECT
		B.*
	FROM
		(SELECT 
			e.emp_no AS employee_ID, 
			MIN(de.dept_no) AS department_code,
				(SELECT 
					emp_no
				FROM 
					dept_manager
				WHERE
					emp_no = 110039) AS manager_ID
		FROM employees e
		JOIN dept_emp de ON e.emp_no = de.emp_no
		WHERE e.emp_no > 10020
		GROUP BY e.emp_no
		ORDER BY e.emp_no
		LIMIT 20) AS B
	UNION SELECT
		C.*
	FROM
		(SELECT 
			e.emp_no AS employee_ID, 
			MIN(de.dept_no) AS department_code,
				(SELECT 
					emp_no
				FROM 
					dept_manager
				WHERE
					emp_no = 110039) AS manager_ID
		FROM employees e
		JOIN dept_emp de ON e.emp_no = de.emp_no
		WHERE e.emp_no = 10022
		GROUP BY e.emp_no) AS C
	UNION SELECT
		D.*
	FROM
		(SELECT 
			e.emp_no AS employee_ID, 
			MIN(de.dept_no) AS department_code,
				(SELECT 
					emp_no
				FROM 
					dept_manager
				WHERE
					emp_no = 110022) AS manager_ID
		FROM employees e
		JOIN dept_emp de ON e.emp_no = de.emp_no
		WHERE e.emp_no = 10039
		GROUP BY e.emp_no) AS D)AS U;
```



thiers:
```mysql
INSERT INTO emp_manager
SELECT 
    u.*
FROM
    (SELECT 
        a.*
    FROM
        (SELECT 
        e.emp_no AS employee_ID,
            MIN(de.dept_no) AS department_code,
            (SELECT 
                    emp_no
                FROM
                    dept_manager
                WHERE
                    emp_no = 110022) AS manager_ID
    FROM
        employees e
    JOIN dept_emp de ON e.emp_no = de.emp_no
    WHERE
        e.emp_no <= 10020
    GROUP BY e.emp_no
    ORDER BY e.emp_no) AS a UNION SELECT 
        b.*
    FROM
        (SELECT 
        e.emp_no AS employee_ID,
            MIN(de.dept_no) AS department_code,
            (SELECT 
                    emp_no
                FROM
                    dept_manager
                WHERE
                    emp_no = 110039) AS manager_ID
    FROM
        employees e
    JOIN dept_emp de ON e.emp_no = de.emp_no
    WHERE
        e.emp_no > 10020
    GROUP BY e.emp_no
    ORDER BY e.emp_no
    LIMIT 20) AS b UNION SELECT 
        c.*
    FROM
        (SELECT 
        e.emp_no AS employee_ID,
            MIN(de.dept_no) AS department_code,
            (SELECT 
                    emp_no
                FROM
                    dept_manager
                WHERE
                    emp_no = 110039) AS manager_ID
    FROM
        employees e
    JOIN dept_emp de ON e.emp_no = de.emp_no
    WHERE
        e.emp_no = 110022
    GROUP BY e.emp_no) AS c UNION SELECT 
        d.*
    FROM
        (SELECT 
        e.emp_no AS employee_ID,
            MIN(de.dept_no) AS department_code,
            (SELECT 
                    emp_no
                FROM
                    dept_manager
                WHERE
                    emp_no = 110022) AS manager_ID
    FROM
        employees e
    JOIN dept_emp de ON e.emp_no = de.emp_no
    WHERE
        e.emp_no = 110039
    GROUP BY e.emp_no) AS d) as u;
```













```
┌─────────────────┐          ┌─────────────────┐
│  employees      ├||──────|<┤  dept_manager   ├>|┐  ┌──────────────────┐
├─────────────────┤          ├─────────────────┤  └||┤   departments    │
│PK mep_no INT    ├||─────┐  │FK dept_no CHAR4 │     ├──────────────────┤
│ birth_date DATE │       │  │FK emp_no INT    │     │PK dept_no CHR4   ├││┐
│ first_name VCHR ├||───┐ │  │ from_date DATE  │     │ dept_name VCHR40 │  │
│ last_name VCHR  │     │ │  │ to_date DATE    │     └──────────────────┘  │
│ gender ENUM     ├||─┐ │ │  └─────────────────┘  ┌────────────────┐       │
│ hire_date DATE  │   │ │ └─────────────────────|<┤   dept_emp     ├>|─────┘
└─────────────────┘   │ │   ┌────────────────┐    ├────────────────┤
  ┌───────────────────┘ └─|<┤     titles     │    │FK emp_no INT   │
  │   ┌────────────────┐    ├────────────────┤    │FK dept_no CHR4 │
  └─|<┤    salaries    │    │FK emp_no INT   │    │ from_date DATE │
      ├────────────────┤    │ title VCHR50   │    │ to_date DATE   │
      │FK emp_no INT   │    │ from_date DATE │    └────────────────┘
      │ salary INT     │    │ to_date DATE   │
      │ from_date DATE │    └────────────────┘
      │ to_date DATE   │
      └────────────────┘
```





















```tikz%
%\documentclass{standalone}
\usepackage{tikz}
\usetikzlibrary{shapes.multipart, positioning, arrows.meta}

\begin{document}
\begin{tikzpicture}[
    node distance=1.5cm and 3cm,
    entity/.style={
        rectangle split,
        rectangle split parts=2,
        draw,
        text width=3.5cm,
        align=left,
        font=\ttfamily,
        minimum height=2cm
    },
    relationship/.style={
        line width=0.8pt,
        draw=black
    }
]

% Entities
\node[entity] (employees) {
    \textbf{employees}
    \nodepart{second}
    PK emp\_no INT \\
    birth\_date DATE \\
    first\_name VARCHAR \\
    last\_name VARCHAR \\
    gender ENUM \\
    hire\_date DATE
};

\node[entity, right=of employees] (dept_manager) {
    \textbf{dept\_manager}
    \nodepart{second}
    FK dept\_no CHAR(4) \\
    FK emp\_no INT \\
    from\_date DATE \\
    to\_date DATE
};

\node[entity, right=of dept_manager] (departments) {
    \textbf{departments}
    \nodepart{second}
    PK dept\_no CHAR(4) \\
    dept\_name VARCHAR(40)
};

\node[entity, below=of dept_manager] (dept_emp) {
    \textbf{dept\_emp}
    \nodepart{second}
    FK emp\_no INT \\
    FK dept\_no CHAR(4) \\
    from\_date DATE \\
    to\_date DATE
};

\node[entity, below=of employees] (titles) {
    \textbf{titles}
    \nodepart{second}
    FK emp\_no INT \\
    title VARCHAR(50) \\
    from\_date DATE \\
    to\_date DATE
};

\node[entity, below=of titles] (salaries) {
    \textbf{salaries}
    \nodepart{second}
    FK emp\_no INT \\
    salary INT \\
    from\_date DATE \\
    to\_date DATE
};

% Crow's foot relationship lines
% Employee to dept_manager (one to many)
\draw[relationship] (employees.east) -- ++(0.2,0) -- ++(0,0.05) -- ++(0,-0.05) -- ++(0.1,0);
\draw[relationship] (employees.east) ++(0.2,0) -- ++(0,-0.05) -- ++(0,0.05);
\draw[relationship] (employees.east) ++(0.3,0) -- (dept_manager.west) ++(0,0) -- ++(-0.3,0);
\draw[relationship] (dept_manager.west) ++(-0.3,0) -- ++(-0.15,0.1);
\draw[relationship] (dept_manager.west) ++(-0.3,0) -- ++(-0.15,-0.1);
\draw[relationship] (dept_manager.west) ++(-0.15,0) -- ++(-0.15,0.1);
\draw[relationship] (dept_manager.west) ++(-0.15,0) -- ++(-0.15,-0.1);

% Department to dept_manager (one to many)
\draw[relationship] (departments.west) -- ++(-0.2,0) -- ++(0,0.05) -- ++(0,-0.05) -- ++(-0.1,0);
\draw[relationship] (departments.west) ++(-0.2,0) -- ++(0,-0.05) -- ++(0,0.05);
\draw[relationship] (departments.west) ++(-0.3,0) -- (dept_manager.east) ++(0,0) -- ++(0.3,0);
\draw[relationship] (dept_manager.east) ++(0.3,0) -- ++(0.15,0.1);
\draw[relationship] (dept_manager.east) ++(0.3,0) -- ++(0.15,-0.1);
\draw[relationship] (dept_manager.east) ++(0.15,0) -- ++(0.15,0.1);
\draw[relationship] (dept_manager.east) ++(0.15,0) -- ++(0.15,-0.1);

% Employee to dept_emp (one to many)
\draw[relationship] ([yshift=-0.3cm]employees.east) -- ++(0.2,0) -- ++(0,0.05) -- ++(0,-0.05) -- ++(0.1,0);
\draw[relationship] ([yshift=-0.3cm]employees.east) ++(0.2,0) -- ++(0,-0.05) -- ++(0,0.05);
\draw[relationship] ([yshift=-0.3cm]employees.east) ++(0.3,0) -- ++(0.7,0) |- ([yshift=0.3cm]dept_emp.west);
\draw[relationship] ([yshift=0.3cm]dept_emp.west) -- ++(-0.15,0.1);
\draw[relationship] ([yshift=0.3cm]dept_emp.west) -- ++(-0.15,-0.1);
\draw[relationship] ([yshift=0.3cm]dept_emp.west) ++(0.15,0) -- ++(-0.15,0.1);
\draw[relationship] ([yshift=0.3cm]dept_emp.west) ++(0.15,0) -- ++(-0.15,-0.1);

% Department to dept_emp (one to many)
\draw[relationship] ([yshift=-0.3cm]departments.west) -- ++(-0.2,0) -- ++(0,0.05) -- ++(0,-0.05) -- ++(-0.1,0);
\draw[relationship] ([yshift=-0.3cm]departments.west) ++(-0.2,0) -- ++(0,-0.05) -- ++(0,0.05);
\draw[relationship] ([yshift=-0.3cm]departments.west) ++(-0.3,0) -- ++(-0.7,0) |- ([yshift=0.3cm]dept_emp.east);
\draw[relationship] ([yshift=0.3cm]dept_emp.east) -- ++(0.15,0.1);
\draw[relationship] ([yshift=0.3cm]dept_emp.east) -- ++(0.15,-0.1);
\draw[relationship] ([yshift=0.3cm]dept_emp.east) ++(-0.15,0) -- ++(0.15,0.1);
\draw[relationship] ([yshift=0.3cm]dept_emp.east) ++(-0.15,0) -- ++(0.15,-0.1);

% Employee to titles (one to many)
\draw[relationship] ([xshift=-0.5cm]employees.south) -- ++(0,-0.2) -- ++(0.05,0) -- ++(-0.05,0) -- ++(0,-0.1);
\draw[relationship] ([xshift=-0.5cm]employees.south) ++(0,-0.2) -- ++(-0.05,0) -- ++(0.05,0);
\draw[relationship] ([xshift=-0.5cm]employees.south) ++(0,-0.3) |- (titles.west);
\draw[relationship] (titles.west) -- ++(-0.15,0.1);
\draw[relationship] (titles.west) -- ++(-0.15,-0.1);
\draw[relationship] (titles.west) ++(0.15,0) -- ++(-0.15,0.1);
\draw[relationship] (titles.west) ++(0.15,0) -- ++(-0.15,-0.1);

% Employee to salaries (one to many)
\draw[relationship] ([xshift=-1cm]employees.south) -- ++(0,-0.2) -- ++(0.05,0) -- ++(-0.05,0) -- ++(0,-0.1);
\draw[relationship] ([xshift=-1cm]employees.south) ++(0,-0.2) -- ++(-0.05,0) -- ++(0.05,0);
\draw[relationship] ([xshift=-1cm]employees.south) ++(0,-0.3) -- ++(0,-1.2) -| (salaries.west);
\draw[relationship] (salaries.west) -- ++(-0.15,0.1);
\draw[relationship] (salaries.west) -- ++(-0.15,-0.1);
\draw[relationship] (salaries.west) ++(0.15,0) -- ++(-0.15,0.1);
\draw[relationship] (salaries.west) ++(0.15,0) -- ++(-0.15,-0.1);

\end{tikzpicture}
\end{document}
```







<u>employees</u>
┌─────────────────┐        ┌─────────────────┐
│  employees                              ├||─|<┤  dept_manager                       ├>|┐  ┌──────────────────┐
├─────────────────┤        ├─────────────────┤   └||┤   departments                             │
│PK mep_no INT                      │        │FK dept_no CHAR4              │        ├──────────────────┤
│ birth_date DATE                    │        │FK emp_no INT                     │        │PK dept_no CHR4                     │
│ first_name VCHR                  │        │ from_date DATE                   │        │ dept_name VCHR40                 │
│ last_name VCHR                   │        │ to_date DATE                       │         └──────────────────┘
│ gender ENUM                       │        └─────────────────┘
│ hire_date DATE                     │
└─────────────────┘

```tikz%
%\documentclass{standalone}
\usepackage{tikz}
\usetikzlibrary{shapes.multipart, positioning, arrows.meta}

\begin{document}
\begin{tikzpicture}[
    node distance=1.5cm and 2.5cm,
    entity/.style={
        rectangle split,
        rectangle split parts=2,
        draw,
        text width=3.5cm,
        align=left,
        font=\ttfamily
    }
]

% Entities
\node[entity] (employees) {
    \textbf{employees}
    \nodepart{second}
    PK emp\_no INT \\
    birth\_date DATE \\
    first\_name VARCHAR \\
    last\_name VARCHAR \\
    gender ENUM \\
    hire\_date DATE
};

\node[entity, right=of employees] (dept_manager) {
    \textbf{dept\_manager}
    \nodepart{second}
    FK dept\_no CHAR(4) \\
    FK emp\_no INT \\
    from\_date DATE \\
    to\_date DATE
};

\node[entity, right=of dept_manager] (departments) {
    \textbf{departments}
    \nodepart{second}
    PK dept\_no CHAR(4) \\
    dept\_name VARCHAR(40)
};

\node[entity, below=of dept_manager] (dept_emp) {
    \textbf{dept\_emp}
    \nodepart{second}
    FK emp\_no INT \\
    FK dept\_no CHAR(4) \\
    from\_date DATE \\
    to\_date DATE
};

\node[entity, below=of employees] (titles) {
    \textbf{titles}
    \nodepart{second}
    FK emp\_no INT \\
    title VARCHAR(50) \\
    from\_date DATE \\
    to\_date DATE
};

\node[entity, below=of titles] (salaries) {
    \textbf{salaries}
    \nodepart{second}
    FK emp\_no INT \\
    salary INT \\
    from\_date DATE \\
    to\_date DATE
};

% Relationships
\draw (employees.east) -- (dept_manager.west);
\draw (departments.west) -- (dept_manager.east);
\draw (employees.east) -| (dept_emp.west);
\draw (departments.west) -| (dept_emp.east);
\draw (employees.south) |- (titles.west);
\draw (employees.south) |- (salaries.west);

\end{tikzpicture}
\end{document}
```












```tikz
\begin{document}
\begin{tikzpicture}[
    % --- DEFINE THE SYMBOLS HERE ---
    one bar/.pic = {
        \draw[thick] (0, -0.15) -- (0, 0.15);
    },
    many circle/.pic = {
        \draw (0,0) circle (0.1cm);
    },
    % --- Style for the table nodes (unchanged) ---
    tbl/.style={
        draw,
        rectangle,
        font=\sffamily\small
    }
]

% --- NODES (Manually placed with coordinates) ---
\node[tbl] at (0,0) (employees) {
    \begin{tabular}{l}
        \textbf{employees} \\ \hline
        PK emp\_no INT \\
        birth\_date DATE \\
        first\_name VARCHAR \\
        last\_name VARCHAR \\
        gender ENUM \\
        hire\_date DATE
    \end{tabular}
};

\node[tbl] at (10,0) (departments) {
    \begin{tabular}{l}
        \textbf{departments} \\ \hline
        PK dept\_no CHAR(4) \\
        dept\_name VARCHAR(40)
    \end{tabular}
};

\node[tbl] at (5, 3) (dept_manager) {
    \begin{tabular}{l}
        \textbf{dept\_manager} \\ \hline
        FK emp\_no INT \\
        FK dept\_no CHAR(4) \\
        from\_date DATE \\
        to\_date DATE
    \end{tabular}
};

\node[tbl] at (5, -3) (dept_emp) {
    \begin{tabular}{l}
        \textbf{dept\_emp} \\ \hline
        FK emp\_no INT \\
        FK dept\_no CHAR(4) \\
        from\_date DATE \\
        to\_date DATE
    \end{tabular}
};

\node[tbl] at (0, -5.5) (titles) {
    \begin{tabular}{l}
        \textbf{titles} \\ \hline
        FK emp\_no INT \\
        title VARCHAR(50) \\
        from\_date DATE \\
        to\_date DATE
    \end{tabular}
};

\node[tbl] at (0, -8.25) (salaries) {
    \begin{tabular}{l}
        \textbf{salaries} \\ \hline
        FK emp\_no INT \\
        salary INT \\
        from\_date DATE \\
        to\_date DATE
    \end{tabular}
};


% --- RELATIONSHIPS (with graphical 'pic' symbols) ---
\draw (employees.east) -| (dept_manager.west)
      pic[pos=0.02, sloped] {one bar}
      pic[pos=0.98] {many circle};

\draw (departments.west) -| (dept_manager.east)
      pic[pos=0.02, sloped] {one bar}
      pic[pos=0.98] {many circle};

\draw (employees.east) -| (dept_emp.west)
      pic[pos=0.02, sloped] {one bar}
      pic[pos=0.98] {many circle};

\draw (departments.west) -| (dept_emp.east)
      pic[pos=0.02, sloped] {one bar}
      pic[pos=0.98] {many circle};

\draw (employees.south) |- (titles.west)
      pic[pos=0.03, sloped] {one bar}
      pic[pos=0.97] {many circle};

\draw (employees.south) |- (salaries.west)
      pic[pos=0.03, sloped] {one bar}
      pic[pos=0.97] {many circle};

\end{tikzpicture}
\end{document}
```