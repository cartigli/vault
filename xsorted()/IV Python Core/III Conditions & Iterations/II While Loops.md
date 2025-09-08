Can be used to achieve the same output as the For Loops but the syntax is slightly refined
ex
```python
x = 0
while x <= 20:
	print(x, end=" ") # this will cause an infinite loop & inevitable crash 
```
Solution: 
	bind x {{x=}} to an operation like +1 to complete after every loop
	as the loop iterates, x gains one per loop and will surpass 20
		{{adding a static variable to the variable x during every iteration is called [Incrementing] - in this example; by 1}}
```python
x = 0
while x <= 20:
	print(x)
	x = x + 1
```
Python has a shorthand for [Incrementing] notation:
```python
x = 0
while x <= 20:
	print(x)
	x += 1 # exactly the same as {{x = x + 1}}