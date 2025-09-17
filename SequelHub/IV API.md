```python
# install library
pip install mysql_connector

# import relevant packages
import mysql.connector


# define the connection to MySQL - in reality will be env variables
conn = mysql.connector.connect( # make connection
	host='192.168.x.xxx', # server host IP
	port=3306, # MySQL default
	user='user_name', # the user you defined / created
	password='pass_word', # associated pass for given user
	database='data_base' # name of target db on the server
)

cursor = conn.cursor() # interactive ' mouse '
cursor.execute("SELECT * FROM table_name") # use the cursor to execute cmd
result = cursor.fetchall() # grab all lines returned from query
print(result)

cursor.close() # close the interactive cursor
conn.close() # close connection to remote server
```
This is the most basic and simplest form of connection 