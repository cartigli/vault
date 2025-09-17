```python
import os
import pandas as pd

file_guts = pd.DataFrame(file_guts, columns=['note_name', 'note_lo', 'note_glory', 'utc_made', 'utc_altered'])#, index = ['note_1', 'note_2']) How do i specify indeterminate indexing? I miss sql.

class file_manager():
	def __init__(self, dir_path, file_guts):
		self.dir_path = dir_path
		self.file_guts = file_guts
						
	def catalog_dir(self, dir_path, files_lo_togo):
		for root, dirs, files in os.walk(dir_path):
			for filename in files:
				full_file_path = os.path.join(root, filename)
				try:
					filenames_togo.append(filename)
					files_lo_togo.append(full_file_path)
				except:
					continue



class server_associate(self, ):
	def __init__(self, ip_addr, pass_w, key):
		self.ip_addr = ip_addr
		self.pass_w = pass_w
		self.key = key

	def initialize_connection():
		ping server
		confirm auth response


class server_liaison(self, ):
	def __init__():

	def pull_db():
		import/pull to database

	def push_db():
		export/push to database


class contractor(self, ):
	def __init__(self, fileguts_togo):
		self.fileguts_togo = fileguts_togo

	def transfer_bulk():
		some sort of better function for sending large files over TCP/API's
```
