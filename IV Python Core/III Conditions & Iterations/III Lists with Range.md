Another built-in Python function is [range()]
```python
range(start, stop, step) # creates a sequence of integers
```
[start] first number in list
[stop] the last value + 1
[step] distance between two consecutive values on the list
	[stop] is required
	[start & step] are optional
		start's default is 0
		step's default is 1
```python
range(10) # same as range(0, 10, 1)
-> range(0, 10)
```
{{ range(0, 10) }} is a range object
	to expand this object, use the list() function:
list(range(10)) 
	{{outputs [1, 2, 3, 4, 5, 6, 7, 8, 9, 10] - a list}}
```python
range(4,9,2)
list(range(4,9,2))
-> [4, 6, 8]
```
all odd numbers 1-30:
	range(1, 30, 2)
	list(range(1, 30, 2)) 
		{{ returns: [1, 3, 5, 7, 9, 11, 13, 15, 17, 19, 21, 23, 25, 27, 29] }}