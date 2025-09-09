Queries complete commands and execute directions, the semi colon stops, or terminates it

Databases
CREATE DATABASE IF NOT EXISTS database_name;
	creates the database under the given name If one does not already under given name

USE database_name;
	specify the database you wish to query

CREATE TABLE table_name (column_names);
	we need to specify column names because no table can be created without names

CREATE TABLE table_name
(
	column_1 data_type constraints,
	column_2 data_type constraints,
	. . .
	column_n data_type constraints
);
```sql
USE sales;

CREATE TABLE sales
(
	purchase_number INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    date_of_purchase DATE NOT NULL,
    customer_id INT,
    item_code VARCHAR(10) NOT NULL
);

CREATE TABLE customers
(
	customer_id INT NOT NULL PRIMARY KEY, --primary key auto increment values 
    first_name VARCHAR(255), --255 char limit with variable length
    last_name VARCHAR(255),
    number_of_complaints INT --integer no comma
);
```

```sql
SELECT * FROM sales; # got table
SELECT customer_id FROM sales; # got row of table
```

```sql
DROP TABLE sales; # tables deleted
```