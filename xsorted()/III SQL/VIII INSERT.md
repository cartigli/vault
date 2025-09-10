We know how to get records, let's make them.

INSERT
Adds values to specified columns of a table.

```mysql
INSERT_INTO table_name (column_1, column_2, . . ., column_n) # state your targets
VALUES (value_1, value_2, . . ., value_n) # fill your targets
```
If we had a table with 5 columns, but we only had 3 worth of data:
```mysql
INSERT INTO table_name (column_1, column_2, column_3)
VALUES (value_1, value_2, value_3) # where values 4 - n would be null
```
*This is fine as long as the column does not have a constraint like NOT NULL. If we specified a different number of columns than the values supplied, more or less, it would return an error. We need not specify all columns of a table, but we must fill all columns we specify.*

