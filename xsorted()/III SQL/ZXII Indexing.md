Indexes
The data is taken from a column of the table and is stored in a certain order in a distinct place; an Index.

Naturally, searching through small databases is relatively easy and cheap resource-wise. Large databases are not like this and slow down incrementally as size grows. To expedite searches, efficiency can be significantly gained with Indexing when finding records within vast collections.

```mysql
CREATE INDEX index_name
ON table_name (column_1, column_2,...);
```
*This is done by column of efficiency of the Index; it should be done on columns where information you search for often resides.*
```mysql
SELECT * FROM employees;
```
*Try some searches before and after indexing the column:*
```mysql
SELECT * FROM employees
WHERE first_name = 'George'
	AND last_name = 'Facello';
```
*Apply the Index:*
```mysql
CREATE INDEX i_hire_date ON employees(hire_date);
```
This was a small database to index, but I still saw a 0.01 second difference in the SELECT * FROM employees query, so the principal is shown. Pretty cool, honestly. Why not index everything always?


Composite Indexes
Applied to *multiple* columns.

```mysql
CREATE INDEX i_hire_date ON employees(first_name, last_name);
```


To see current Indexes:
```mysql
SHOW INDEX FROM database_name FROM table_name;
```
*For the ones made above:*
```mysql
SHOW INDEX FROM employees FROM employees;
```