```python
def areaAndperimeter(x):
	if x > 0:
		A = x ** 2
		B = x * 8
		print('Area and Perimeter')
		print(A,B)
		return A,B
	elif x < 0:
		print('Negative entries are invalid')
	else:
		print('0 is 0 is 0 is 0...')

areaAndperimeter(9)
areaAndperimeter(-9)
areaAndperimeter(0)
```
