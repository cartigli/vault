[Iteration] is the ability to execute certain code repeatedly 
	fundamental to all programming

Iteration Process:

[for loop]
```python
even = [0,2,4,6,8,10,12,14]
for n in even: # for every element n in the list even:
	print(n) # n is the loop variable
```
The loop iterates through every element in the list: even, until it finishes all elements and exits the loop
	{{one completed loop is called an [Iteration Pass]}}
	{{n could be x or y or z or monkey_brains}}
```python
for n in even:
	print(n, end=" ") # print them all, continue until the end {{which is nothing}}
```
^^this is so the outputs will all be entered on the same line
** for the terminal on my personal pc, the Python instance had trouble outputting all of this loop above^^
	to resolve, the loop was modified to the iteration below which repaired the missing Elelements
```python
for n in x:
	print(n, end=" ")
print()
```
then, the output is: [1, 2, 3, 4, 5] instead of [>>>3, 4, 5]