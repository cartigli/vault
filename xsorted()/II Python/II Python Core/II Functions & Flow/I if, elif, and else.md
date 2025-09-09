If statements are intuitive;
	{assigns a Boolean value to your query

[ Conditionals ]
if 5 != 5 * 3:
	print('Hello, world')
-> Hello, world

if 5 > x and y <= 4:
	print('Both variables fit')
[ Else ]
Else runs a block of code if the preliminary if statement is false
```python
if x > 1:
	print('Case 1')
else:
	print('Case 2')
```

[ Elif ]
Another conditional after a preliminary if statement
```python
def comparefive(x):
     if x > 5:
         print('Greater')
     elif x < 5:
         print('Less')
     else:
         print('Equal')
comparefive(6)
-> Greater
comparefive(4)
-> Less
comparefive(5)
-> Equal
```