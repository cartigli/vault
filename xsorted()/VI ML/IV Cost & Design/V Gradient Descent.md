the original , most fundamental Optimization Algorithm

[ Gradient Descent ] is the multivariate generalization of the derivative of the [ Cost Function ]

quick derivatives :
	$f(x) = 3x^2 + 5x + 1$
	$f'(x) = 2*3x + 5 + 0$
		$f'(x) = 6x + 5$
			*the derivative is denoted with : '
				*the derivative of f(x) is f'(x)*

suppose we want to find the minimum of the function : $x$ {{ above }}
	if we used the gradient slope method
		we take the derivative 
			$f'(x) = 6x + 5$
		we generate a random number to start
			x = 7
		and determine accuracy
-
		then, we update the model, given the new loss
			$x_0 = 7$
			$x_1 = ?$
			$x_{i+1} = x_i - \eta f'(x_i)$
			$x_{1} = x_0 - \eta f'(x_0)$
			$x_{1} = 7 - \eta f'(7)$
			$x_{1} = 7 - \eta(47)$
$$\eta=\text{Learning Rate}$$
						*let's make eta, or $\eta = 0.01$
				$x_{1} = 7 - (0.01 * 47)$
				$x_{1} = 7 - 0.47$
				$x_{1} = 6.53$
		*we choose the learning rate for each case*
			eventually, the values will stop decreasing , which is the minimum cost
				the derivative = the slope of a function , so when the derivative of our loss function is 0 , we know the cost is at a minimum
```python
import numpy as np
import pandas as pd

# f_x = 3x^2 + 5x + 1
# f'_x = 6x + 5
# update rule: x_i+1 = x_i - eta ( x_i )

x = np.randn([42])

def update_w(x_out, eta)
	x_i = x
	x_ii = x_i - eta*x_i
	x_ii = x
	return x

f_x = 3*[x**2]+5x+1

def looper(x, eta, f_x)
	if x > -1000:
		f_x(x) = x_out
		x_new = update_w(x_out, 0.01)
		print(x_out, x_new)
	return x_out, x_new