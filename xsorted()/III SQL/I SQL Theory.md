Declarative Language { non-procedural }
	focus on what you want as the end goal, not the path taken to achieve it
		Done through the SQL Optimizer

SQL's Syntax is comprised of:
	Data Definition Language [ DDL ]
	Data Manipulation Language [ DML ]
	Data Control Language [ DCL ]
	Transaction Control Language [ TCL ]

SQL's Syntax:
[ DDL ] set of statements that allows the user to define or modify data structures and objects, such as tables
	CREATE : used for creating databases or tables 
		CREATE object_type object_name;
		CREATE table object_name (column_name, data_type);
			"CREATE table sales (purchase_num, int);" creates one table of the name sales with one row; purchase_num that is comprised of only integers
			table name can coincide with the database name without issues and is common
	ALTER : modifies existing object ; add, remove, rename
		 "CREATE table sales (purchase_num, int); 
		ALTER TABLE sales
		ADD COLUMN data_of_purchase DATE;"
			this modifies the sales column by adding a column of DATES
	DROP : can remove existing tables or columns or contents
	TRUNCATE : remove existing data from table without removing table
		"TRUNCATE TABLE sales" would clear the table of its values
	ADD : can add an entity
		"ADD COLUMN revenue"

[ DML ] statements that allow manipulation of data in databases or tables
	SELECT :
		"SELECT * FROM sales" extracts all data from table
	INSERT :
		"INSERT INTO sales (columns, specified) VALUES (values, for, specified, columns)"
			need to specify the column you want the data unless you'd like them added to all values in the table
		INSERT is closely connected to INTO and VALUES
	UPDATE : modify current values
		"UPDATE sales 
			SET date_of_purchase = '17/12/21' WHERE purchase_num = 1;"
				" set the row with date_of_purchase equal to 17/12/21 to be purchase number 1 under purchase_num
					replace whatever purchase_num is currently associated with 17/12/21 with 1"
	DELETE : like TRUNCATE but more specific
		"DELETE FROM sales;" would have the same effect as TRUNCATE
		"DELETE FROM sales
			WHERE purchase_num = 1;" only deletes the row of the table from which purchase_num equals 1
	{ SELECT... FROM..., INSERT INTO... VALUES, UPDATE... SET... WHERE, DELETE... FROM... WHERE }

[ DCL ] less common ; only two statements, controls access of users
	GRANT gives or grants permissions to users
		"GRANT type_of_permission ON database_name.table_name TO 'user@localhost'"
			"GRANT SELECT ON  sales.customers TO joe@localhost"
				Now, Joe can only run the select command, not TRUNCATE, DELETE, or INSERT
			"GRANT ALL ON  sales.* TO joe@localhost"
				Now, Joe can run all and any queries on any database or table within sales
	REVOKE

[ TCL ] 
	When editing a database, the alteration or implementation to the database will only be shown globally when COMMIT is used ; reverting the commit is done with ROLLBACK;
		COMMIT 's cannot be changed and are permanent 
		ROLLBACK undos alterations up until the last COMMIT

SQL Keywords : ADD, CREATE, ALTER
	objects or databases cannot be named these as they are used by SQL
	