Interacting with and opening files with Python.

open( ) is a built-in function
```python
open(file_path, access_mode)
```
Access modes: 
	   r = read only
		 w = opens a file to write only, makes a file if doesn't exist

Ok, this is much simpler than I expected

```python
with open(file_path, 'r') as file:
	line_count = 0
	for line in file:
		line_count += 1
	return line_count
```


```python
import os  
  
# Get the current working directory  
current_directory = os.getcwd()  
print(f"Current working directory: {current_directory}")  
  
# List contents of a directory  
contents = os.listdir(current_directory)  
print(f"Contents of current directory: {contents}")

os.walk()
```

```python
import os

for root, dirs, files in os.walk('/Volumes/HomeXx/compuir/vault/xsorted()/III SQL'):
	print(f"{root}, {dirs}, {files}")
```


Count file lengths recursively through a given folder:
```python
import os

file_path = '/Volumes/HomeXx/compuir/vault'

line_cnt_list = []

for root, dirs, files in os.walk(file_path):
	for filename in files:
		full_file_path = os.path.join(root, filename)
		try:
			with open(full_file_path, 'r') as file:
				line_count = 0
				for line in file:
					line_count += 1
				line_cnt_list.append(line_count)
		except:
			continue

line_cnt_list.sort()

print(max(line_cnt_list))
print(line_cnt_list)
```

Count characters recursively through a given folder:
```python
import os

file_path = '/Volumes/HomeXx/compuir/vault/xVault'

char_cnt_list = []

for root, dirs, files in os.walk(file_path):
	for filename in files:
		full_file_path = os.path.join(root, filename)
		try:
			with open(full_file_path, 'r') as file:
				char_count = 0
				for line in file:
					char_count += len(line)
				char_cnt_list.append((char_count, filename))
		except:
			continue

char_cnt_list.sort()

print(max(char_cnt_list))
print(char_cnt_list)
```

7,861,302