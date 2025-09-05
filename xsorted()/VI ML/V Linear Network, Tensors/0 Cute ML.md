```python
import numpy as np
import pandas as pd

# f_x = 3x^2 + 5x + 1
# f'_x = 6x + 5
# update rule: x_i+1 = x_i - eta ( x_i ) 

x = 222
epochs = 100
learning_rate = 0.1

#def f(x):
#	return 3*x**2+5*x+1

def f_prime(x):
	return 6*x+5

def train(x, epochs):
	print(f"Epoch Count:{epochs},\nInitial x:{x}\n\n")
	for i in range(epochs):
		gradient = f_prime(x)
		x = x - learning_rate*(gradient)
		#for i in range(epochs): was printing x 50 times per epoch lol
		if i % 20 != 0:
			print(f"epoch {i}:,{x:.2f}")
	return x

print(train(x, epochs))
```