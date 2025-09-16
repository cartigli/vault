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

Macos / brew installation:
brew install mysql { installs mysql }
brew install --cask mysqlworkbench { installs the application workbench }
mysql.server start { initializes the server }
mysql -u root -p { starts session with the server via the terminal }

MySQL Permissions
To allow my.sql to load local files { not a containerized instance }, edit the conf in the brew collection:
```
nano /opt/homebrew/etc/my.cnf
# add this line to the bottom the file:
secure-file-priv = ""
```
*You could also specify a directory to give access between the quotes here as well. Leaving them empty gives MySQL access to all of your folders and files.*

Make a database & test loading_file function:

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

The plain text worked, the file given with file path / name did not. Also, given that MySQL ate these special characters without issue, we can be sure we do not need to worry about the content of the text when loading it into a database. There is, however, an issue with special characters in titles, or at least for what I am working on.

The script below prints out queries that initially configure a database but more importantly iteratively create insert statements for each file in a given folder. Since MySQL is taking these filenames and paths verbatim and specifying with ' ' { single quotes }, filenames, and therefor paths, with apostrophes will cause errors. They will appear in the Insert command and break the continuum of the intended string. They should either be removed or renamed before running this script.

```python
# Orchestrator
import os

file_path_g = '/Volumes/HomeXx/compuir/vault/xVault'
file_path_s = '/Volumes/HomeXx/compuir/vault/xsorted()'

print(f"CREATE DATABASE IF NOT EXISTS notes_db;\nUSE notes_db;")

print(f"CREATE TABLE IF NOT EXISTS note_ \n(\nnote_no INT NOT NULL PRIMARY KEY AUTO_INCREMENT,\ntitle VARCHAR(75) NOT NULL,\npath VARCHAR(255) NOT NULL,\nnote TEXT NOT NULL CHARACTER SET utf8mb4\n);")

for root, dirs, files in os.walk(file_path_g):
	for filename in files:
		full_file_path = os.path.join(root, filename)
		try:
			if filename.startswith("."):
				print("# Not for the db")
			else:
				print(f"INSERT INTO note_ (title, path, note)\nVALUES ('{filename}','{full_file_path}', LOAD_FILE('{full_file_path}'));")
		except:
			continue

for root, dirs, files in os.walk(file_path_s):
	for filename in files:
		full_file_path = os.path.join(root, filename)
		try:
			if filename.startswith("."):
				print(f"# Not for the db")
			else:
				print(f"INSERT INTO note_ (title, path, note)\nVALUES ('{filename}','{full_file_path}', LOAD_FILE('{full_file_path}'));")
		except:
			continue
```

This script takes the two given directories and searches for every file within them using os.walk( ). The conditional the function is built around first checks if the filename begins with a '.' and if True, then it prints "# Not for the db" as it is likely a .git or .obsidian file { Python will ignore characters after the '#' }. Either way or a third, it is not a note of mine. If the value is False, the loop moves to print the Insert statement for the given file. The table, whose configuration is in the top print statement, holds the columns note_no, title, path, and note. The Primary Key, note_no, is set to Auto_Increment, so regardless of whether it is specified or not, it will not be Null and it will automatically increment as consecutive records are added. Title is a Varchar of 75 characters because the titles range significantly in length and can be fairly long. Its probably excessive but more for demonstration and testing than a practical application, for now. Path is configured similarly but with a longer range because the path is considerably long in some folders.

The note column is constrained by a datatype of Text. This limits the characters added to this column to 65,535 characters, or about 64 kb of storage. This is also just over the longest note in my vault. I found this through a loop which originally counted the lines of the files in a given folder { this is also the foundation of the loop logic above } and returned a sorted list of the folder's files' line-counts. Instead of 'for line in file: line_count += 1', 'for line in file: len(file)' was used to find the characters in each line of each file, which was then summed. This script is below.

```python
import os

file_path = '/Volumes/HomeXx/compuir/vault'

char_cnt_list = []

for root, dirs, files in os.walk(file_path):
	for filename in files:
		full_file_path = os.path.join(root, filename)
		try:
			with open(full_file_path, 'r') as file:
				char_count = 0
				for line in file:
					char_count += len(line)
				char_cnt_list.append(char_count)
		except:
			continue

char_cnt_list.sort()

print(max(char_cnt_list))
print(char_cnt_list)
```

With the given limit found, the Text type was chosen and the utf encoding was the final configuration for the table. Additionally, every column in the table is set to Not Null because no note can exist without the path, and no file can be loaded without the filename, so there will not be a need for safety nets within this table. Plus, better for peace of mind.

Finally, to get the script with the queries to configure the database, table, and MySQL environment, run the script titled 'Orchestrator' as a .py file in the terminal. On Macos, after making the .py file and ensuring you are in the same directory as said file, run "python3 script.py > script.sql". You will see no output in the terminal and a new file will be created: scripts.sql. Open workbench and load the file into the UI, which upon completion will show you a series of executable queries that will load the entire file you specified into the database and table of your choosing.

Notes: you must complete the modification to the MySQL config file described above under 'MySQL Permissions'. Only after doing so will the MySQL instance be able to recognize and read files on your local machine. Additionally, perhaps this is an obvious detail, but on Windows, running the .py file with the python command is 'python script.py > script.sql'; '3' is not needed as it is with Macos' implementation with Python.