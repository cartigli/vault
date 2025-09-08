```python 
def raise_to_three(x):
	return x**3

print(raise_to_three(3))

lambda x: x**3 # expression, parameter, function

raise_to_lambda = lambda x: x**3

print(raise_to_lambda(3))

# you can also give it the input right after declaring the function of lambda
print((lambda x: x / 2 ) (11))

print((lambda x: x**3 / x**2 ) (4))

# can do multiple variables
print((lambda x, y: x**y) (3,2))

sumxy = lambda x,y: x + y
print(sumxy(4,5))

