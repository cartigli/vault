``
							OLS Regression Results                            
================================================

                  coef    std err    t     P>|t|    [0.025    0.975]
-----------------------------------------------------------------------------
const {b0}     0.2750      0.409      0.673      0.503      -0.538       1.088
 SAT  {b1}     0.0017      0.000      7.487      0.000       0.001       0.002
================================================
Coefficients Table:
	Coefficient Column:
		const: shows the y intercept, or constant, of the LR
				coeff, constant, and bias are interchangeably used
				$\beta_0$ ; in the example above, $\beta_0 = 0.2750$
		x-variable: shows the slope of line of best fit for the regression
				coeff var is the y-hat for our model; $\beta_1$
				y-hat = $\beta_0$ + {{x-var/$\beta_1$}} * x1
					in the case above, $\beta_1 = 0.0017$
							$\hat{y} = \beta_0 + \beta_1 * x1$
							$\hat{y} = 0.2750 + 0.0017 * x1$
		Std err:
				accuracy of prediction for every variable x
				lower this value, higher the accuracy of the model
			t-score:
				means hypothesis is a part of this course; null hypothesis is equal to 0 {{ $H_0 : \beta = 0$ } = is the coefficient of the model equal to 0? } so it determines the usability of the slope of the model. Does it answer the variability? No, p-value does.
			p-value:
				shows the variability of the model; >0.05 is a significant value
				the SAT-p-value is less than 0.05, so it is a significant variable when calculating GPA's
				if the p value were over 0.05, the value of the variable would not be significantly different from 0
				