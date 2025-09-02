Non linear ; duh
predicts the probability of an event occurring
		given {{ input data }}, what is the probability of admission?

The curve is called a Logistic Regression curve
The method of prediction is Logistic Regression

Function of a Logistic Regression:
$p_x = \frac{e^{B_0 + B_1 * x_1 + . . . B_k * x_k}}{1 + e^{B_0 + B_1 * x_1 + . . . B_k * x_k}}$
			The probability of x occurring is equal to: {{ $e^{B_0 + B_1 * x_1 + . . . B_k * x_k}$}} , divided by {{ 1 + $e^{B_0 + B_1 * x_1 + . . . B_k * x_k}$}}


With transformation and swapping, we can get the Logit Regression Model:
$\frac{p_x}{1 - p_x} = e^{B_0 + B_1 * x_1 + . . . B_k * x_k}$
			The probability of x occurring divided by one minus the probability of x occurring is equal to the exponent from above
			a.k.a.: ' odds '
						Ex: tossing a coin;
								if I call heads, the probability of getting heads is equal to heads divided by 1 - p(tails)
								or 50 / 50, 
								or 1 to 1
						Rolling a dye:
								if I want a 6, the probability og getting a 6 is the probability of rolling a six over the probability of not rolling a 6
								probability of 6 = 1/6, so:
								1/6 / { 1 - 1/6 } = 1/6 / { 5/6 } = 1:5

logarithmic functions are the counterpart to exponents, so...
take the log of both sides of the Logit Regression Model:
$\log(\frac{p_x}{1 - p_x}) = \log(e^{B_0 + B_1 * x_1 + . . . B_k * x_k})$
$\log(\frac{p_x}{1 - p_x}) = B_0 + B_1 * x_1 + . . . B_k * x_k$
$\log(odds) = B_0 + B_1 * x_1 + . . . B_k * x_k$
			The log of the Logit Regression model makes the calculations identical to the linear function, but with log applied to the ' odds '