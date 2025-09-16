We know how to get records, let's make them.

INSERT INTO
Adds values to specified columns of a table.

```mysql
INSERT_INTO table_name (column_1, column_2, . . ., column_n) # state your targets
VALUES (value_1, value_2, . . ., value_n) # fill your targets
```
*If we had a table with 5 columns, but we only had 3 worth of data:*
```mysql
INSERT INTO table_name (column_1, column_2, column_3)
VALUES (value_1, value_2, value_3) # where values 4 - n would be null
```
*This is fine as long as the column does not have a constraint like Not Null. If we specified a different number of columns than the values supplied, more or less, it would return an error. We need not specify all columns of a table, but we must fill all columns we specify.*
```mysql
INSERT INTO table_name(
	emp_no,
	birth_date,
	first_name,
	last_name,
	gender,
	hire_date
) VALUES(
	99901,
	'1986-04-21',
	'John',
	'Smith',
	'M',
	'2011-01-01'
);
```
*However, naming all columns isn't essential.*
```mysql
INSERT INTO employees
VALUES (
	99902,
	'1956-10-12',
	'James',
	'Lasagna',
	'M',
	'2007-04-29' );
```
*The above would work as long as the table we are inserting into has the same amount of columns of values we are trying to insert and ordered in the specified manner.*


INSERT INTO { from another table's values }

```mysql
INSERT INTO table_2 (column_1, column_2, . . ., column_n)
VALUES (value_1, value_2, . . ., value_n)
FROM table_1
WHERE *condition[s]*;
```
*Allows insertion of data to a table from another tables' values given some condition.*
```mysql
CREATE TABLE duplicate_depts (
	dept_no CHAR(4) NOT NULL,
	dept_name VARCHAR(40) NOT NULL ); # make a new table to move the data to

SELECT * FROM duplicate_depts; # ensure it is empty

INSERT INTO duplicate_depts # since we have itentical columns & names
SELECT * FROM departments; # we don't need to specify values, columns, or conditions
```


Transactional Control Lock and Rollback
Similar to Github, the Commit locks in a change, and the Rollback clause reverts the database to its last Commit. Unlike Github, if you have made 10 Commits, you may only Rollback to the latest Commit. By default, MySQL uses auto-commit mode. ##**How do transactions work?**##

```mysql
ROLLBACK;
COMMIT;
```
*If no Commits have been made, rolling back will revert the database to its initial state. Rollback's are irreversible.*


UPDATE
Updates values of existing records in a table.

```mysql
UPDATE table_name
SET column_1 = value_1, column_2 = value_2 . . .
WHERE *condition[s]*;
```
*This is used to update a table or columns of a table based on and restricted by a given condition.*
```mysql
# 999901 was John Smith, let's replace him
UPDATE employees
SET
	first_name = 'Jennifer',
	last_name = 'Ortega',
	birth_date = '1999-03-03',
	gender = 'F'
WHERE
	emp_no = 999901; # set it to update the record corresponding to emp_no 999901
```
*This removes John Smith from the employees table and replaces him with Jennifer Ortega. If the where clause was referencing a non-existent value, as in there were no employee with the emp_no 999901, this would return an error.*
	*If no condition or Where clause is given, the update cmd will update & replace all rows of the given table.*


DELETE
Removes records from a database.

```mysql
DELETE FROM table_name
WHERE *condition[s]*
```

```mysql
DELETE FROM employees
WHERE emp_no = 999903;
```
*This deletes the record of the employee from the table employees. If this value corresponds to another table in which the constraint On Delete Cascade was set, said value from corresponding table will also be deleted when the above is executed.*
	*Again, if no condition is set or given, this command will be applied to the entire table.*

DROP vs TRUNCATE vs DELETE
Drop removes a table's structure, contents, and records entirely. It is permanent. Truncate is a statement that wipes a table of its records while the table remains and Auto Incrementing values are reset. Delete removes records row by row and only those corresponding to the given condition. Without a condition, or removing all records from a table, is much faster with Truncate as it does not operate row by row. Furthermore, the Auto Incrementing values are not reset with Delete; if the previous contents had reached 13, the new value for the empty table with Delete will be 14.