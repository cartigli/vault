We can pick p-many elements in as many ways as we can pick n minus p-many elements 

	|
	|     x
	|   x x x
y_axis| _ x x x x x _ x_axis

y = C(n, p) 
x = 0 - n
C(n, p) has symmetry over n/2
Combinations are maxed when n/2 = p

Ex: 3 [p] of 10 [n] employees for conference 
C(10, 3) = 120
if 7, C(10, 7) = 120
So; picking 7 combinations of people to go to the conference is the same as picking 3 combinations to stay/go
They are symmetrical across the example graph above

Maximum Combinations [n/2]: C(10, 5) = 10! / (10 - 5)! 5!
	C(10, 5) = 10! / (5!) 5!
	C(10, 5) = 6 x 7 x 8 x 9 x 10 / 5!
	C(10, 5) = 6 x 7 x 8 x 9 x 10 / 1 x 2 x 3 x 4 x 5
	C(10, 5) = 6 x 7 x 8 x 9 x 10 / 5!
	C(10, 5) = 30240 / 120 
	C(10, 5) = 252
