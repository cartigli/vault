when two or more variables have high correlation
$P_{x_i,x_j} \approx 1 : \forall i, j; i \neq j$

if $a = 2 + 5 * b$ , and $b = a - 2 / 5$
			they can be completely and perfectly represented solely between themselves 
			$P_{ab} = 1$ ; or perfect multicollinearity
						if a can be represented using b, and b can be represented using a, there is no point in using both
			if $P_{cd} = 0.9$ ; also multicollinearity and poses a problem for our model, but not perfect 

two bars, Bonkers and Shakespeare 
			they want to find a model that can predict their market shares; if one bars prices increase or decrease, the likely outcome is the other bar matching to maintain competitiveness
						because the prices of the bars follow each other, modeling this behavior is not for statistical regression and confuses the outcome of the model

Solutions:
		drop one of two variables
		transform both variables into one variable