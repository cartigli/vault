def function_name(parameters):
	function body

function_name(parameters) {returns output of function body}

function_name(10)
10 is an [argument], not a parameter of the function 'function_name'

def funct(a):
	result = a / 7
	return result 
		{add a function in a function, and return its output}

Limited by the [Parameters]
```python
def minus_bc(a,b,c):
	result = a - b * c
	print('Parameter a ', a)
	print'(Parameter b ', b)
	print'(Parameter b ', c)
	return result
```
minus_bc(4,3,2)
	{returns 4 - 3 * 2; -2}

minus_bc(b=4,a=5,c=2)
	{returns 5 - 4 * 2; -3}

Note**
	a function should use print(data) to show Humans the resulting data, and return {{ data }} should be used when returning the function's output to whatever called the function originally; returns it to code so it can keep using it