function that counts the numbers who are less than 20 from a list
Called a [ Rolling Sum ]
```python
def count(numbers):
	total = 0
	for x in numbers:
		if x < 20:
			total = total + 1
	return total
```
{{ if x is less than 20, one is added to the total {which starts at 0}, if x is greater than 20, the function does nothing }}
```python
n = [1,2,3,4,5,29,54,18,19,30]
count(n)
-> 7
```
