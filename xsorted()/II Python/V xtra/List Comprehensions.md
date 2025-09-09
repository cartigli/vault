```python
num = [2,13,7,36,42]

new_num = [] # empty list

for n in num:
	new_num.append(n/2)

print(new_num)

new_num = [n*2 for n in num]
print(new_num)

for i in range(3):
	for j in range(4):
		print(i+j, end=" ")
print('\n')

new_n = [i+j for i in range(3) for j in range(4)]
print(new_n) # list vs nested loop was not

new_n1 = [[i+j for i in range(3)] for j in range(4)]
print(new_n1) # four sets of 3 :)

next = [test/2 for test in new_n if test % 2 != 0]
print(next)
print(type(next)) # list of odd numbers in newn divided by 2

next = [test/2 if test % 2 != 0 else "even" for test in new_n]
print(next)
print(type(next)) # same but if not satisfactory for conditional, replace with ' even ' 