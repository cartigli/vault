```python
import os
import pandas as pd
import mysql.connector
#from config import * # import env variables from env file

# in place of future env file
USER = 'root'
PASS_PHRASE = 'koipo222'
DATABASE_NAME = 'employees'
TABLE_NAME = 'employees'
DATABASE_ADDR = '192.168.1.68'
HOST_PORT = 3306
#ALLOWED_PACKETS = 67108864
LOCAL_DIR = '/home/tom/vault'

def initialize_connection(USER, PASS_PHRASE, DATABASE_NAME, TABLE_NAME, DATABASE_ADDR, HOST_PORT):
	conn = mysql.connector.connect(
		host=DATABASE_ADDR,
		port=HOST_PORT,
		user=USER,
		password=PASS_PHRASE,
		database=DATABASE_NAME,
		#max_allowed_packet=ALLOWED_PACKETS
		)
	return conn

conn = initialize_connection(USER, PASS_PHRASE, DATABASE_NAME, TABLE_NAME, DATABASE_ADDR, HOST_PORT)
cursor = conn.cursor()

conn.execute(f"SELECT * FROM employees;")
conn.fetchall()

#print(con.fetchall())
```