SELECT
Allows extraction of and interaction with portions of the dataset.

```mysql
SELECT column_1, column_2, column_3 . . . 
FROM table_name;
```
*Collect all employees names:*
```mysql
SELECT first_name, last_name FROM employees;
```
*With formatting:*
```mysql
SELECT 
	first_name, last_name 
FROM 
	employees;
```
*Or collect all columns from employees table with an asterisk:*
```mysql
SELECT * FROM employees;
```


WHERE
Sets condition on what will be retrieved from the database.

```mysql
SELECT column_1, column_2, column_3 . . . 
FROM table_name
WHERE condition;
```

```mysql
SELECT * FROM employees WHERE first_name = 'Denis';
```
*Will return only values where the condition is met ; i.e., records where the first name's value is Denis*
	' = ' is an operator, meaning equals. Operators are used with WHERE
		There is also AND, OR, IN, LIKE, BETWEEN, NOT IN, NOT LIKE, AND, etc.,


AND
Allows you to combine two statements in the condition block ; it narrows the returned data.

```mysql
SELECT column_1, column_2, column_3 . . . 
FROM table_name
WHERE condition_1 AND condition_2;
```

```mysql
SELECT * FROM employees
WHERE first_name = 'Elvis' AND gender = 'F';
```
*Both criteria must be met for data to be returned from the query.*


OR
Like AND but the opposite.

```mysql
SELECT * FROM employees
WHERE first_name = 'Elvis' OR first_name = 'Denis';
```
*Returns all the names of records in employees who have the name Elvis OR the name Denis.
```mysql
SELECT * FROM employees
WHERE first_name = 'Elvis' AND first_name = 'Denis';
```
Would likely return nothing as there is a low likelihood of someone having two first names.


ORDER PRECEDENCE
SQL rule stating in the execution of a query, the operator AND is applied first, before the OR operator.

```mysql
SELECT * FROM employees
WHERE 
	last_name = 'Denis' 
AND 
	gender = 'F' OR gender = 'M'; # operator on both sides
```
*This returns all records from employees where the last name recorded is Denis AND the gender is Male OR Females, so we got all the values of Male Denis's and then got all the Females recorded in employees regardless of their name.*
In order to set precedence other than the default order, SQL requires parenthesis:
```mysql
SELECT * FROM employees
WHERE 
	last_name = 'Denis' 
AND 
	(gender = 'F' OR gender = 'M');
```
*This modifies the previous query to return only people whose last name is Denis and is either female or male.*
```mysql
SELECT * FROM employees
WHERE 
last_name = 'Denis'
	OR last_name = 'Cathy'
	OR last_name = 'Dorothy'
```
*Looks for people in employee named Denis or Cathy or Dorothy, returns values that satisfy any of the three conditionals.*


IN | NOT IN
With more than two conditions to be satisfied, IN | NOT IN are more appropriate AND or OR.

```mysql
SELECT * FROM employees
WHERE 
last_name IN ('Denis', 'Cathy', 'Dorothy');
```
*This does the same as the overdone OR operators in the query above this one, but cleaner and considerably faster.*
```mysql
SELECT * FROM employees
WHERE 
last_name NOT IN ('Denis', 'Cathy', 'Dorothy');
```
*This would return all the employees in the database whose first name is NOT Denis, Cathy, or Dorothy.*


LIKE | NOT LIKE
To exclude or include values that follow an indicated pattern.

```mysql
SELECT * FROM employees
WHERE first_name LIKE ('Mar%'); # returns first names of which start with 'Mar'
```
*Returns first names of which start with 'Mar'* - *% is a substitute for the following for preceding letters of a value.*
```mysql
SELECT * FROM employees
WHERE first_name LIKE ('%ar');
```
*Returns first names of which end with 'Ar'.*
```mysql
SELECT * FROM employees
WHERE first_name LIKE ('%ar%');
```
*Returns first names of which contain the string 'ar'.*
```mysql
SELECT * FROM employees
WHERE first_name LIKE ('Mar_');
```
*Returns only the first names in employees of which contain four letters and start with 'Mar'.*
	*Returns Marv, Mark, Mary, etc.,*
```mysql
SELECT * FROM employees
WHERE first_name NOT LIKE ('%Mar%');
```
*Returns all the values of first names of which do not contain anywhere within themselves the string 'mar'. Cases are not considered in MySQL unless configured to be so.*


WILDCARD CHARACTERS
" % " , " * " , " _ "
" % " serves as a substitute for a varying amount of symbols preceding or following the given string.
" _ " serves as a placeholder for a single symbol, it works the same as ' % ' but with no varying length of symbols.
" * " serves as a wildcard only for the SELECT query's target.

BETWEEN
Always used with the AND operator.
*Remember that the AND operator holds precedence and is considered before other operators.*

```mysql
SELECT * FROM employees
WHERE
	hire_date BETWEEN '1990-01-01' AND '2000-01-01';
```
*Returns all employees who were hired between Jan 1st, 1990, and Jan 1st, 2000.*
```mysql
SELECT * FROM employees
WHERE
	hire_date NOT BETWEEN '1990-01-01' AND '2000-01-01';
```
*Returns all employees hired BEFORE Jan 1st, 1990 and AFTER Jan 1st, 2000.*


IS NULL | IS NOT NULL
Enforces a state on the column to be created or altered. Null is the default.

```mysql
SELECT * FROM employees
WHERE first_name IS NOT NULL;
```
*Returns the values of first_name's from the employees table in which name is not null.*
```mysql
SELECT * FROM employees
WHERE first_name IS NULL;
```
*Returns the values of first_name's from the employees table in which name is null - shows the counterpart to the query above.*
	*One can find all values of a column or data type that are null or not null*
```mysql
SELECT emp_no, first_name FROM employees
WHERE first_name IS NOT NULL;
```
*Returns all the employee numbers and first names of all employees whose first name is not null.*


ADD. COMPARISON OPERATORS
' = ' , ' > ' , ' >= ' , ' =< ' , ' < ' , ' <> ' , ' != '
{ " = " : equal, " > " : greater than, " > = " : greater than or equal, " < " : less than, " < = " : less than or equal, " < > " : not equal, " ! = " : not equal }

NOT EQUAL : { < > } or { ! = } = not equal, different from
```mysql
SELECT * FROM employees WHERE first_name = 'Mark'; # find all those named Mark

SELECT * FROM employees WHERE first_name <> 'Mark'; # find all those NOT named Mark ; also could be !=
```

AFTER : { > } after is denoted with the ' greater than ' symbol
```mysql
SELECT * FROM employees WHERE hire_date > '2000-01-01'; # find all those hired AFTER the specified date
```

BEFORE : { < } before is the counterpart of AFTER
```mysql
SELECT * FROM employees WHERE hire_date < '2000-01-01'; # find all those hired BEFORE the specified date
```


SELECT DISTINCT
```mysql
SELECT gender FROM employees; # returns all entries in the gender column
SELECT DISTINCT gender FROM employees; # returns only one M and one F ; or all the distinct values in gender
```


AGGREGATE FUNCTIONS
Applied on multiple rows of a single column of a table and return an output of a single value.


COUNT()
Counts the number of Non-Null records in a field.

```mysql
SELECT column_name COUNT(column_name)
FROM # returns two rows ; first with each group of unique values
	table_name; # second, it returns an additional column with the number of values in each row
```

```mysql
SELECT COUNT(emp_no)
FROM employees;
```
*This counts all the rows of the emp_no column from the employees table. emp_no = primary key, so we know it won't repeat and don't need DISTINCT.*

```mysql
SELECT COUNT(DISTINCT first_name)
FROM employees;
```
*Find all the employees unique names within the column first_name and returns the list.*
```mysql
SELECT COUNT(*) FROM salaries WHERE salary >= 75405;
```
*Returns all salaries from the table Salaries where the value in column salary is over or equal to $75,405.*

SUM()
Sums all the Non-Null values in a column.

MIN() & MAX()
Returns the minimum or maximum value from the entire list.

AVG()
Calculates the average of all the Non-Null values belonging to a specified column of a table.

ORDER BY
```mysql
SELECT * FROM employees;
```
*Returns massive amounts of data, so:*
```mysql
SELECT * FROM employees 
ORDER BY first_name;
```
*Returns same amount of data but more organized output.*
```mysql
SELECT * FROM employees 
ORDER BY first_name ASC;
```
*ASC is Ascending order, which is also the default for the ORDER BY operator.*
```mysql
SELECT * FROM employees 
ORDER BY first_name DESC;
```
*DESC is the counterpart to ASC, this specifies in Descending order.*
```mysql
SELECT * FROM employees 
ORDER BY emp_no DESC;
```
*Works on numeric values as well as string values.*
```mysql
SELECT * FROM employees 
ORDER BY first_name, last_name ASC;
```
*This orders the employees returned initially by first names, and for matching names, it orders them in ascending order within those names.*


GROUP BY
Results can be grouped according to a specific field or fields.

```mysql
SELECT (column_name[s]) FROM table_name
WHERE
	*conditions*
GROUP BY
	column_name[s]
ORDER BY
	column_name[s];
```

```mysql
SELECT first_name FROM employees
GROUP BY first_name;
```
*Returns all unique first_names; multiple of the same name are grouped together on a single row, so the length of the return will be equal to the COUNT DISTINCT of the given column. Names will not be shown, only the amount of observations for each returned value.*
	*GROUP BY must be placed immediately after any WHERE conditions, if present, and just before any ORDER BY clauses, if present.*
```mysql
SELECT first_name, COUNT(first_name) FROM employees
GROUP BY first_name
ORDER BY first_name ASC;
```
*Returns the count of the first_names from the employees table and groups them by first name, which is ordered by first name.*


ALIAS
```mysql
SELECT first_name, COUNT(first_name) AS names_count # add an alias
FROM employees
GROUP BY first_name
ORDER BY first_name;
```
*This returns the same as the previous query but the title over the count of the first names will be titled ' names_count ' instead of COUNT(first_name).*


HAVING
Refines the outputs from records that do not satisfy a certain condition - like WHERE, but applied to the GROUP BY block.
```mysql
SELECT 
	column_name[s]
FROM
	table_name
WHERE
	*condition[s]*
GROUP BY
	column_name[s]
HAVING
	*condition[s]*
ORDER BY
	column_name[s];
```
*Comparison of uses:*
```mysql
SELECT salary FROM salaries
WHERE hire_date > '1999-01-01' # filters BEFORE grouping
GROUP BY salary ORDER BY salary;
```

```mysql
SELECT dept_no, COUNT(*) AS emp_count FROM employees
GROUP BY dept_no
HAVING COUNT(*) > 50; # COUNT(*)>50 is applied to the returned data AFTER grouping
```
*The former returns employees hired after Jan 1st, 1999 and sorts them into groups of salaries by their salaries. The latter selects the department No. and the count of employees but keeps only the departments who have over 50 employees **after** the column is selected and the HAVING COUNT( * ) > 50 is satisfied.*
```mysql
SELECT employee_id, AVG(salary) FROM salaries
GROUP BY employee_id
HAVING AVG(salary) <= 65000; # filters AFTER grouping
```
*HAVING's unique application is it can have aggregate functions for its conditions, where as WHERE cannot. Its use is for sorting or applying new conditions after the GROUP BY's return is pulled back.*

Suppose you wanted to find all the employees names of which appear more than 250 times in the employees table:
```mysql
SELECT first_name, COUNT(first_name) AS names_count FROM employees
GROUP BY first_name
HAVING 
	COUNT(first_name) > 250 # this is proper syntax and will execute correctly
ORDER BY first_name;
```
*Count is an aggregate function, so to include it as a conditional in a query, you must use HAVING, not WHERE.*

Retrieve the average contract salary for each employee whose average salary is higher than $70,000. Sort the output by employee number in ascending order. Solution:
```mysql
SELECT emp_no, AVG(salary) FROM salaries
GROUP BY emp_no
HAVING AVG(salary) > 70000
ORDER BY emp_no ASC;
```
*Returns a list of two columns; first is employee number is ascending order and the other is AVG(salary) of the referenced employee.*


WHERE
Allows setting of conditions that refer to subsets of individual rows. It is applied before re-organizing the output into groups.
	*WHERE sets the conditions upon the table so the only returned values match said condition. After this, the WHERE clause looses its power and HAVING comes in.

HAVING allows us to set a condition AFTER the values that satisfy the prerequisite conditions are met. After retrieval, HAVING applies some additional condition to the retrieved data.

Imagine we need to extract a list of all names that are encountered less than 200 times. Let the data refer to people hired after the 1st of January, 1999. 
```mysql
SELECT first_name, COUNT(first_name) AS names_count FROM employees
WHERE hire_date > '1999-01-01'
GROUP BY first_name
HAVING COUNT(first_name) <= 200
ORDER BY first_name;
```


LIMIT
```mysql
SELECT * FROM salaries; # could return thousands of lines
```

```mysql
SELECT * FROM salaries
limit 10; # limits response to 10 rows
```
*Ex: looking for top 10 salaries within the company:*
```mysql
SELECT salary FROM salaries
ORDER BY salary DESC 
LIMIT 10;
```
*This returns the top average salaries sorted by descending order limited to 10 rows.*

Overarching guide to syntax we've seen so far:
```mysql
SELECT 
	column_name[s]
FROM
	table_name
WHERE
	*condition[s]*
GROUP BY
	column_name[s]
HAVING
	*condition[s]*
ORDER BY
	column_name[s]
LIMIT
	10;
```