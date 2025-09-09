SELECT - Allows extraction of portions of the dataset

```mysql
SELECT column_1, column_2, column_3 . . . 
FROM table_name;
```

Ex : collect all employees names
```mysql
SELECT first_name, last_name FROM employees;
```

Or with formatting:
```mysql
SELECT 
	first_name, last_name 
FROM 
	employees;
```

Or : Collect all columns from employees table with an asterisk
```mysql
SELECT * FROM employees;
```


WHERE - Sets condition on what will be retrieved from the database

```mysql
SELECT column_1, column_2, column_3 . . . 
FROM table_name
WHERE condition;
```

Like :
```mysql
SELECT * FROM employees WHERE first_name = 'Denis';
```
*Will return only values where the condition is met ; i.e., records where the first name's value is Denis*
	' = ' is an operator, meaning equals. Operators are used with WHERE
		There is also AND, OR, IN, LIKE, BETWEEN, NOT IN, NOT LIKE, AND, etc.,

AND - Allows you to combine two statements in the condition block ; narrows returned data

```mysql
SELECT column_1, column_2, column_3 . . . 
FROM table_name
WHERE condition_1 AND condition_2;
```

Like :
```mysql
SELECT * FROM employees
WHERE first_name = 'Elvis' AND gender = 'F';
```
*Both criteria must be met for data to be returned from the query*


OR

```mysql
SELECT * FROM employees
WHERE first_name = 'Elvis' OR first_name = 'Denis';
```
*Returns all the names of records in employees who have the name Elvis OR the name Denis

```mysql
SELECT * FROM employees
WHERE first_name = 'Elvis' AND first_name = 'Denis';
```
Would likely return nothing as there is a low likelihood of someone having two first names


ORDER PRECEDENCE - SQL rule stating in the execution of a query, the operator AND is applied first, before the OR operator

```mysql
SELECT * FROM employees
WHERE 
	last_name = 'Denis' 
AND 
	gender = 'F' OR 'M';
```
*This returns all records from employees where the last name recorded is Denis AND the gender is Male OR Females, so we got all the values of Male Denis's and then got all the Females recorded in employees regardless of their name*

In order to set precedence other than the default order, SQL requires parenthesis
```mysql
SELECT * FROM employees
WHERE 
	last_name = 'Denis' 
AND 
	(gender = 'F' OR 'M');
```
*This modifies the previous query to return only people whose last name is Denis and is either female or male*

```mysql
SELECT * FROM employees
WHERE 
last_name = 'Denis'
	OR last_name = 'Cathy'
	OR last_name = 'Dorothy'
```
*Looks for people in employee named Denis or Cathy or Dorothy, returns values that satisfy any of the three conditionals*


IN | NOT IN - With more than two conditions to be satisfied, IN | NOT IN are key
	Allows SQL to return the names in parentheses if they exist in our database

```mysql
SELECT * FROM employees
WHERE 
last_name IN ('Denis', 'Cathy', 'Dorothy');
```
*This does the same as the overdone OR operators in the query above this one, but cleaner and considerably faster*

```mysql
SELECT * FROM employees
WHERE 
last_name NOT IN ('Denis', 'Cathy', 'Dorothy');
```
*This would return all the employees in the database whose first name is NOT Denis, Cathy, or Dorothy*


LIKE | NOT LIKE - To exclude or include values that follow an indicated pattern

```mysql
SELECT * FROM employees
WHERE first_name LIKE ('Mar%'); # returns first names of which start with 'Mar'
```
*Returns first names of which start with 'Mar'* - *% is a substitute for the following for preceding letters of a value*

```mysql
SELECT * FROM employees
WHERE first_name LIKE ('%ar');
```
*Returns first names of which start with 'Ar'*

```mysql
SELECT * FROM employees
WHERE first_name LIKE ('%ar%');
```
*Returns first names of which contain the string 'ar'*

```mysql
SELECT * FROM employees
WHERE first_name LIKE ('Mar_');
```
*Returns only the first names in employees of which contain four letters and start with 'Mar'* 
	*Returns Marv, Mark, Mary, etc.,*

```mysql
SELECT * FROM employees
WHERE first_name NOT LIKE ('%Mar%');
```
*Returns all the values of first names of which do not contain anywhere within themselves the string 'mar'*

WILDCARD CHARACTERS
`'%', '*', & '_'`
% serves as a substitute for a varying amount of symbols preceding or following the given string

' * ' serves as a true wildcard, returning any and all subsequent records

' _ ' serves as a placeholder for a single symbol, it works the same as ' % ' but with no varying length of symbols


BETWEEN - Always used with the AND operator
	*Remember that the AND operator holds precedence and is considered before other operators*

```mysql
SELECT * FROM employees
WHERE
	hire_date BETWEEN '1990-01-01' AND '2000-01-01';
```
*Returns all employees who were hired between Jan 1st, 1990, and Jan 1st, 2000*

```mysql
SELECT * FROM employees
WHERE
	hire_date NOT BETWEEN '1990-01-01' AND '2000-01-01';
```
*Returns all employees hired BEFORE Jan 1st, 1990 and AFTER Jan 1st, 2000*