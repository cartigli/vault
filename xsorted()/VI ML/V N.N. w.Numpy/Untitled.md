```python
import numpy as np
import pandas as pd

# f_x = 3x^2 + 5x + 1
# f'_x = 6x + 5
# update rule: x_i+1 = x_i - eta ( x_i ) 

x = 222
epochs = 100
learning_rate = 0.1

def f(x):
	return 3*x**2+5*x+1

def f_prime(x):
	return 6*x+5

#def update_w(gradient, learning_rate=0.01):
#	return learning_rate*gradient

def train(x, epochs):
	print(f"Epoch Count:{epochs},\nInitial x:{x}\n\n")
	for i in range(epochs):
		gradient = f_prime(x)
		x = x - learning_rate*(gradient)
		#for i in range(epochs): was printing x 50 times per epoch lol
		if i % 20 != 0:
			print(f"epoch {i}:,{x.:2f}")
	return x

print(train(x, epochs))
```





















```
# i abandoned this once I was in teh weeds

x = np.random.randn(42)
epoch_c = 100

def f(x):
	return 3*x**2 + 5*x + 1

def f_prime(x):
	return 6*x + 5

def update_w(x_, learning_rate=0.1): # this returns the new x value ; i thught.
    return learning_rate*x_ # eta x f'(x)

def training_loop(x): # goal here was to have the model run x , get an output, get the gradient for updating weights ; i guess i am not comparing to find accuracy in the first place. I understand the minimum is at 5/6ths, but I want the model to find it. 
	for i in range(epoch_c):
		x_ = f_prime(x) # so I could add to update weight, but it already uses f_prime and only takes x
		x = x_ - update_w(x_)
	return x

print(training_loop(x))