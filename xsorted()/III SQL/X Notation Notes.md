```mysql
CREATE table if not exists text (numbers int(10), words varchar(10));
```
with the above formatting + add. uniformity 
```mysql
CREATE TABLE IF NOT EXISTS text
(
	numbers    INT(10),
	words      VARCHAR(10)
);
```
also :
```mysql
CREATE TABLE IF NOT EXISTS text
(
numbers
	INT(10),
words
	VARCHAR(10)
);
```

BREW:
mysql.server start { initializes the database }

mysql -u root -p { starts CLI session with the server }

Change file permissions on sql server:
	Edit the conf in the brew collection:
```
nano /opt/homebrew/etc/my.cnf
# add this line to the bottom the file:
secure-file-priv = ""
```
*You could also specify a directory to give access between the quotes here as well.*
Make a database & test loading_file function 
```mysql
CREATE DATABASE IF NOT EXISTS note_pad;

DROP TABLE n1;

USE note_pad;

CREATE TABLE n1
(
	note_no INT AUTO_INCREMENT NOT NULL,
    title VARCHAR(75), 
    notes TEXT,
PRIMARY KEY (note_no)
) CHARACTER SET utf8mb4;

INSERT INTO n1
VALUES (2, 'test2', LOAD_FILE('/Volumes/HomeXx/compuir/vault/xVault/miscellaneous/les fleures.md'));

INSERT INTO n1
VALUES (1, 'test', 'This is my test text for the sql vault of ** MY ** super fun and weirdly \\\\\\ strange character ridden \\\\\\\\\\\\\\\\\ ///////////////// text, so lets see \\\\\\\\\\\\\\nwhat NySQK doES!!!!************');


SELECT * FROM n1;

SHOW VARIABLES LIKE 'secure_file_priv';
```
*The plain text worked, the file given with file path / name did not.*