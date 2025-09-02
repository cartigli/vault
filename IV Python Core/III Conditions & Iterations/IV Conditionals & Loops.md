combine [for loops] and [range functions]
```python
for n in range(10):
	print(2 ** n, end=" ") # output on a single line
-> 4 9 16 25 36 49 64 81 100
```
Create a loop that prints all evens between 0-19 and state the evens
```python
for x in range(20):
	if x % 2 < 1:
		print('Even found: ',str(x))
	else:
		print('Oddball Mother Fucker...',str(x))
```
worked! {{ adding , end=" ") to the print expressions did force all outputs to the same line }}