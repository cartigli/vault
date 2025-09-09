Applications in Data Science
	[ vectorized code ]
	[ image recognition ]
	[ dimensionality reduction ]

[ vectorized code ]
	claim: house price depends on size
		you devlop this equation:
		House Price = 10,190 + 223 x K[sq ft]
			A calculation for the price of five houses is as follows"
				10,190 + 223 x 693[k] = 164,729
				10,190 + 223 x 474[k] = 115,892
				10,190 + 223 x 892[k]= 209,106
				10,190 + 223 x 556[k] = 134,178
				10,190 + 223 x 1275[k] = 294,515
			but also could be a loop:
```python
import numpy as np

x = (693, 474, 892, 556, 1275)
price_dhouses = []

for i in x:
	p = 10190 + (223*i)
	price_dhouses.append(p)
print(price_dhouses)

# or 
price_houses=[10190 + ( 223 * i ) for i in x]
print(price_houses)
```

OR : consider two matrices, 5x2 & 2x1
$$A = \begin{bmatrix}
 1 & 693 \\ 1 & 474 \\ 1 & 892 \\ 1 & 556 \\ 1 & 1275  \end{bmatrix} ; B = \begin{bmatrix} 10190 \\ 223 \end{bmatrix}$$
 Their Dot Product :
 $$\begin{bmatrix}
 1 & 693 \\ 1 & 474 \\ 1 & 892 \\ 1 & 556 \\ 1 & 1275  \end{bmatrix} \cdot \begin{bmatrix} 10190 \\ 223 \end{bmatrix} = \begin{bmatrix} 1*10,190 + 223*693 \\ 1*10190 + 223*474 \\ 1*10190 + 223*892 \\ 1*10190 + 223*556 \\ 1*10190 + 223*1275 \end{bmatrix} = \begin{bmatrix} 164,729 \\ 115,892 \\ 209,106 \\ 134,178 \\ 294,515 \end{bmatrix}$$
 we got the same result!
	 oversimplifying the concept of ML, we could call matrix A the inputs, and matrix B the weights, or coefficients
		 we applied the weights of 10,190 and 223 to the input matrix cleanly!

* if we had $1000$ inputs, in the shape of $1000x2$, we could still apply this matrix of $2x1$ as its weights! The result would be a $1000x1$ matrix :)

when we use array programming to compute linear algebraic expressions, it is called [vectorizing code]

[ image recognition ]
	take a 400x400 pixel image
	together, we see this is an image, with a subject, color, etc.,
		it could also be expressed as a matrix, an array of 400x400 pixels
			if we gray-scaled the photo, we could give every pixel a rating for the intensity of the darkness for that pixel
			then, the 400x400 matrix's values would be comprised of every pixel's intensity, or the gray-scaled photo - this is something the machine can ' see '
				could train it to classify dogs, burglars, birds, etc.,
			if we wanted color, instead of the matrix being 400x400x1 { intensity of gray } , we could do 400x400x3 [Tensor], where the resulting additional dimensions held information about that pixel's RGB scale, to simulate authentic colors

[ dimensionality reduction ]
not going in, only intuition
	essentially, like matrices, a series of points can be shown over 3 dimensions but if the points form a plane, or approximate one, we could call it a new plane and remove a dimension from its form ; reducing its dimensionality