Main difference between Lists and Tuples is Tuples are immutable
	they cannot be changed or modified, hence:
		.append or .extend do not work with Tuples

difference between a Tuple and List is Tuples use immutable 
x = (1, 2, 3) {{this is a Tuple}}
x = [ 1, 2, 3 ] {{this is a List}}
	this is the default bundling of objects for Python;
	x = 1, 2, 3 {they are automatically bundled into a Tuple}
	x 
	> (1, 2, 3) {will be output as the Tuple}
		indexing works here, so to find the index of an object in x;
		x[1] {would return 2, the object with the index value of 1}

a, b, c = 1, 2, 3 {{assigns each variable to one value; Tuple assignment}}
b
-> 2

Can make a list of Tuples, where an object in the list is a Tuple
x = 1, 2, 3
y = 4, 5, 6
Tuple_list = [x,y]
Tuple_list {{outputs [ (1, 2, 3) (4, 5, 6) ]}}

(age, year) = "40,1999".split(',')
	the Tuple age, year gets assigned the values 40, 1999 with the proper notation inside the .split() method, which respectively assigns the values to the Tuple of age, year, splitting them on the ',' symbol
	print(age)
	-> 40
	print(year)
	-> 1999
```python
# Functions can also return Tuples
def area_perim(x):
	A = x ** 2
	B = x * 8
	print('Area and Perimeter')
	return A,B

area_perim(5)
-> Area and Perimeter
-> (25, 40)
```