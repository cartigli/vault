consider $x$
$f(x) = y$, but we don't know this function yet

how can we have the algorithm find it?
	we give it pairs of inputs and outputs to try to decipher a pattern or develop an algorithm to determine the function
	1=f(0.5)
	1.21 = f(0.22)
	1.33 = f(0.11)
	5.21 = f(2.1)
	2.22 = f(12.27)
	0 = f(0)
		this is the training data the model will ' learn ' from ; its task is to find the hypothesis function f(x) from this set of sample values of f(x)

This could be done with a [Linear Model]
	These models use the equation $f(x) = x \cdot w + b$
		*obviously $y = m \cdot x + b$*, but in ML terms :
			$f(x) = x \cdot \text{weights[w]} + \text{bias[b]}$
				The goal of the ML algorithm would be to find values for w & b such that any value of x would equal the correct output of the training data of the original function ; or as closely fit as possible 
					{{ least inaccuracy / closest to all points }}

*If this were a real estate - prediction model , its would be likely given x , where x = size , and w and b are configured to predict the price of a house given the size , x

[ Multiple Variables Linear Model ]
What if we're determining cost of houses in Charleston?
	An additional element for location would be introduced 
		In the single variable model, the input $x$ is a $1x1$ scalar being multiplied with a $1x1$ scalar, added to a $1x1$ scalar
			*In this example*, $x$ has an additional element, location, so it is $1x2$
				To be compatible for the dot product, w needs to be in the shape $2x1$
					x.shape = $1x2$ and w.shape = $2x1$ would equal a scalar as the result ; $2x1$ by $1x2$ would result in a matrix
						Then, the bias can remain a scalar as they can be added to vectors and matrices
```python
import numpy as np

x = [2, 3]
w = [1.2, -3]
b = [7]
z = np.dot(x,w) + b
print(z)
```

[ Multivariable Linear Model with Multiple Outputs ]
Imagine our model designed to predict the price of houses in Charleston was also tasked with determining the rent price?
	Without modifying the input or training data, the model would need to predict two things:
			The price of the house
			The cost of renting the same house
				$Y_1$ : the price as a function of the size of the house and proximity to the beach
				$Y_2$ : the rent as a function of the size of the house and proximity to the beach
									$Y_1 = X_1 * W_{11} + X_2 * W_{21} + B_1$
									$Y_2 = X_1 * W_{12} + X_2 * W_{22} + B_2$
										$W_{11}$ - refers to : {{ first 1 = refers to x ; second 1 = refers to Y }}
											for rent, $Y_1 \text{ becomes : } Y_2$ , so $W_11 \text{ becomes : } W_12$ {{ x did not change }}
											** *if we have K inputs and M outputs, we need K x M Weights and M Biases* **
								$Y_1, Y_2$ = 2 Outputs {{ M }}
								$X_1, X_2$ = 2 Inputs {{ K }}
									$W_{11}, W_{21}, W_{12}, W_{22}$ = 4 Weights {{ K x M }}
									$B_1, B_2$ = 2 Weights {{ M }}

$Y_1 = X_1 * W_{11} + X_2 * W_{21} + B_1$
$Y_2 = X_1 * W_{12} + X_2 * W_{22} + B_2$

$X_1, X_2$ = 743, 1.2
$$\begin{bmatrix} X_1 & X_2 \end{bmatrix} = \begin{bmatrix} 743 & 1.2 \end{bmatrix} = \text{Inputs}$$
$$\begin{bmatrix}
404 & 14 \\ -15,512 & -484 \end{bmatrix} = \begin{bmatrix} W_11 & W_12 \\ W_21 & W_22 \end{bmatrix} = \text{Weights}$$
$$\begin{bmatrix} B_1 & B_2 \end{bmatrix} = \begin{bmatrix} 1,113 & 212 \end{bmatrix}=\text{Biases}$$
$$Y_1 = 743 * 404 + 1.2 * -15,512 + 1,113$$$$Y_2 = 743 * 14 + 1.2 * -484 + 212$$
$$Y_1 = 30,0172 - 18,614 + 1,113$$$$Y_2 = 10,402 - 581 + 212$$
$$Y_1 = 282,671 \text{ : Prediction of House Price}$$$$Y_2 = 10,033 \text{ : Prediction of House Rent}$$

This works for correlations that adhere mostly to a straght line, for example, the scatter plot below
```python
import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(-6,6,100)

y = -(x**2) + 4

plt.figure(figsize=(6,7))

plt.plot(x, y, color='purple',linewidth=1) # plt.plot() connects the points

plt.title('linear vs non-linear functions')
plt.xlabel('y=mx+b')
plt.ylabel('y=-(x^2)+b')

plt.xlim(-10,10)
plt.ylim(-10,10)
plt.grid(True)
plt.axhline(0, color='black',linewidth=0.5) # h for horizontal @ 0
plt.axvline(0, color='black',linewidth=0.5) # v for vertical @ 0

plt.show()
plt.close()
```