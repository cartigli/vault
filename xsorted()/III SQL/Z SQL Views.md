A virtual table whose contents are obtained from an existing table or tables; contains no physical data but simply shows the data contained in the base table. 
	They are helpful because if using large databases and viewed by many, instead of rerunning select queries every time a user wants to see this data, they can instead just access the view. It is updated as information in the database is added and modified, but it itself cannot be modified by adding or removing records.

```mysql
CREATE VIEW view_name AS
SELECT column_one, column_2,...
FROM table_name;
```
*Acts as a shortcut for writing Select commands.*
```mysql
CREATE VIEW v_dept_latest_date AS 
SELECT emp_no, MAX(from_date) AS from_date, MAX(to_date) AS to_date
FROM dept_emp
GROUP BY emp_no;
```
*Create Or Replace is like the Create If Not Exists from previously in the section.*
```mysql
DROP VIEW IF EXISTS v_name;
```