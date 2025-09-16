Specific limitations or specifications applied to a table
	outlines the relationships between tables

PRIMARY KEY
```mysql
CREATE TABLE sales
(
	purchase_number INT AUTO_INCREMENT,
	date_of_purchase DATE,
	customer_id INT,
	item_code VARCHAR(10),
PRIMARY KEY (purchase_number)
);
```

A child table references with a Foreign Key a to a Parent Table
	Usually, this Parent Table's value is a Primary Key for the parent
		The foreign key maintains the referential relationship within the database

```mysql
CREATE TABLE sales
(
	purchase_number INT AUTO_INCREMENT,
	date_of_purchase DATE,
	customer_id INT,
	item_code VARCHAR(10),
PRIMARY KEY (purchase_number),
FOREIGN KEY (customer_id) REFERENCES customers(customer_id) ON DELETE CASCADE # foreign key constraint
);
```

*On Delete Cascade - this constrains the tables by defining a rule enforcing the child table to delete all associated records with a customer_id if a value of the Primary Key on the Parent Table is deleted.*

```mysql
CREATE TABLE sales
(
	purchase_number INT AUTO_INCREMENT,
	date_of_purchase DATE,
	customer_id INT,
	item_code VARCHAR(10),
PRIMARY KEY (purchase_number)
);

ALTER TABLE sales
ADD FOREIGN KEY (customer_id) REFERENCES customers(customer_id) ON DELETE CASCADE; # add key after the fact

ALTER TABLE sales
DROP FOREIGN KEY sales_ibfk_1; # to remove key
```

UNIQUE KEYS

```mysql
CREATE TABLE customers
(
	customer_id INT,
	first_name VARCHAR(255),
	last_name VARCHAR(255),
	email_address VARCHAR(255),
	number_of_complaints INT,
PRIMARY KEY (customer_id),
UNIQUE KEY (email_address)
);
```
*Add after the fact:*
```mysql
CREATE TABLE customers
(
	customer_id INT,
	first_name VARCHAR(255),
	last_name VARCHAR(255),
	email_address VARCHAR(255),
	number_of_complaints INT,
PRIMARY KEY (custumer_id)
);

ALTER TABLE customers
ADD UNIQUE KEY (email_address);
```


PRIMARY, FOREIGN, AND UNIQUE
```mysql
CREATE TABLE products
(
    product_id INT AUTO_INCREMENT,
    product_name VARCHAR(20),
    product_price INT,
    warehouse_id INT,
PRIMARY KEY (product_id),
FOREIGN KEY (warehouse_id) REFERENCES warehouse(warehouse_id),
UNIQUE KEY (product_name)
);
```

INDICES
Unique keys serve the same role is indexes , but not the reverse! Indexing allows organization and retrieval of information and enforces updating of all indices if one is updated.
```mysql
ALTER TABLE customers
DROP INDEX email_address; # drop index , not unique key , and remove parenthesis
```

DEFAULT CONSTRAINT
ex: No. of Complaints would default to 0 unless specified otherwise.
```mysql
CREATE TABLE customers
(
	customer_id INT AUTO_INCREMENT,
	first_name VARCHAR(255),
    last_name VARCHAR(255),
    email_address VARCHAR(255),
    number_of_complaints INT DEFAULT 0,
PRIMARY KEY (customer_id)
);
```
*Add in hindsight:*
```mysql
ALTER TABLE customers
CHANGE COLUMN number_of_complaints number_of_complaints INT DEFAULT 0; # sets default value to 0
```
*Remove after the fact:*
```mysql
ALTER TABLE customers
ALTER COLUMN number_of_complaints DROP DEFAULT; # sets default to null
```

```mysql
CREATE TABLE products
(
    product_id INT AUTO_INCREMENT,
    product_name VARCHAR(20) DEFAULT 'no-name',
    product_price INT,
    warehouse_id INT,
PRIMARY KEY (product_id),
FOREIGN KEY (warehouse_id) REFERENCES warehouses(warehouse_id),
UNIQUE KEY (product_name)
);
```

NOT NULL
Constrains the given column to not accept Null values.

```mysql
CREATE TABLE products
(
    product_id INT AUTO_INCREMENT,
    product_name VARCHAR(20) DEFAULT 'no-name',
    product_price INT,
    warehouse_id VARCHAR(255) NOT NULL, # enforces values for every position
PRIMARY KEY (product_id),
);
```
*To remove constraint:*
```mysql
ALTER TABLE companies
MODIFY warehouse_id VARCHAR(255) NULL; # removes NOT NULL enforcement
```
*To add in hindsight:*
```mysql
ALTER TABLE companies
CHANGE COLUMN warehouse_id warehouse_id VARCHAR(255) NOT NULL; # adds NOT NULL enforcement rule
```

*Null values should not be confused with 0 or None.
	No. of Complaints : 0 means zero complaints filed, null would mean we have no information on whether or not this record has any or ever filed complaints.*

INSERT VALUES { WITH ENUM & PRIMARY KEY }

```mysql
USE sales;

CREATE TABLE customers
(
	customer_id INT AUTO_INCREMENT,
	first_name VARCHAR(255),
    last_name VARCHAR(255),
    email_address VARCHAR(255),
    number_of_complaints INT,
PRIMARY KEY (customer_id)
);

ALTER TABLE customers
ADD COLUMN gender ENUM('M','F') AFTER last_name; # only 'M' or 'F' permitted

INSERT INTO customers (first_name, last_name, gender, email_address, number_of_complaints)
VALUES ('John','Mackinley','M','john.mickinley@365careers.com',0);

INSERT INTO customers (first_name, last_name, gender, email_address)
VALUES ('Jane','Mackinley','F','jane.mickinley@365careers.com'); # no value or reference for default
```