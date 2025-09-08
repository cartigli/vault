[ Sequences ] = Tuples, Lists ; order is determined by position of element within the sequence
```python
t = (3,4,5,6)
f = [2,3,4,5]

#for i in t:
#	print(i)

#for i in f:
#	print(i)


#for i in range(5.0):
#	print(i)

# nested loops
#for i in range(2):
#	print(i)

#for j in range(5):
#	print(j)

#for i in range(2):
#	for j in range(6):
#		print(j)

#for i in range(2):
#	for j in range(6):
#		print(i)


#for i in range(2):
#	for j in range(6):
#		print([j,i])

#for i in range(2):
#	for j in range(6):
#		print([i,j])

for i in ['rats','dogs']:
	for j in ['dogs','rats']:
		print([i,j])


animals = ['cats','dogs','lions','rats']

for i in animals:
	for j in animals:
		print([i,j])

print('\n\n')
# triple nested loops
products = ['product a','product b']
exp_sales = [10000,11000,13000,11000,12000]
time_horiz = [1,3,12]

for i in products:
	for j in exp_sales:
		for k in time_horiz:
			#print([i,j*k]) # each products expected sales for the next time horizons
			print('Expected sales for product {}, for time horizon of {} month[s]: ${sales}'.format(i,k,sales=k*j))