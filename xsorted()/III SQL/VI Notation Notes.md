```sql
CREATE table if not exists text (numbers int(10), words varchar(10));
```
with capitalization & structure
```sql
CREATE TABLE IF NOT EXISTS text
(
	numbers INT(10),
	words VARCHAR(10)
);
```
with the above formatting + add. uniformity 
```sql
CREATE TABLE IF NOT EXISTS text
(
	numbers    INT(10),
	words      VARCHAR(10)
);
```

BREW:
mysql.server start { initializes the database }

mysql -u root -p { starts CLI session with the server }