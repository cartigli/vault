Matrix: a collection of numbers ordered in rows and columns
An example of a matrix:
$$A = \begin{bmatrix}
1 & 3 & 5 \\
7 & 10 & 1
\end{bmatrix}$$
	this matrix has 6 elements
		matrices are usually denoted with capital letters
			matrix A has 2 rows and 3 columns, 
				or A is a 2 x 3 matrix
					or $A_{2x3}$

Matrices hold values for mathematically operations, unlike a table
Matrices can be added, subtracted, multiplied, and divided
	they can only contain numbers, symbols, or expressions, so long as the latter 2 are representational of numeric values

generalized shape/size:
	$A_{MxN}$ has the shape m rows and n columns
		to specify a certain element of a matrix $A_{MxN}$, one can find the needed element with this notation:
			$a_{ij}$ where i denotes the $i^{\text{th}}$ row and j denotes the $j^{\text{th}}$ column ; like x-y positioning
				continuing, the $1^{\text{st}}$ position of the $1^{\text{st}}$ row and $1^{\text{st}}$ column is $a_{11}$
					the last item of the $1^{\text{st}}$ column is $a_{m1}$ 
						the last item of the $1^{\text{st}}$ row is $a_{n1}$
							the last item of the matrix is $a_{mn}$
			**This is for math notation!! In python, the specifications of elements in the matrix are the EXACT SAME, BUT with m & n -1 for every position.**
						$a_{ij}$ where i denotes the $i-1^{\text{th}}$ row and j denotes the $j-1^{\text{th}}$ column {{ similar to x-y positioning }}
									continuing, the $1^{\text{st}}$ position of the $1^{\text{st}}$ row and $1^{\text{st}}$ column is $a_{00}$

Because I am a brick brained boy, here's a note for order of notation for describing a matrices' shape:
	ROWS x COLUMNS
	HIEGHT x WIDTH
	HIEGHT $1^{\text{st}}$ x WIDTH $2^{\text{nd}}$