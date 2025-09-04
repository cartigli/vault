```python
import numpy as np
import pandas as pd

# f_x = 3x^2 + 5x + 1
# f'_x = 6x + 5
# update rule: x_i+1 = x_i - eta ( x_i )

x = np.random.randn(42)
epoch_c = 100

def f(x):
	return 3*x**2 + 5*x + 1

def f_prime(x):
	return 6*x + 5

def update_w(x_, learning_rate=0.1):
    return learning_rate*f_prime(x)

def training_loop(x):
	for i in range(epoch_c):
		x_ = f_prime(x)
		x = x_ - update_w(x_)
	return x

print(training_loop(x))
```