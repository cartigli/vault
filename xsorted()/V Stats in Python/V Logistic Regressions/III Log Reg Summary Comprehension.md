```
                            Logit Regression Results                           
===========================================================================
Dep. Variable:               Admitted   No. Observations:                  168
Model:                          Logit   Df Residuals:                      166
Method:                           MLE   Df Model:                            1
Date:                Sun, 31 Aug 2025   Pseudo R-squ.:                  0.7992
Time:                        21:33:51   Log-Likelihood:                -23.145
converged:                       True   LL-Null:                       -115.26
Covariance Type:            nonrobust   LLR p-value:                 5.805e-42
```

Interpretation:
		Method: MLE
				Maximum Likelihood Estimation ; estimates how likely it is that the model underhand describes the real, underlying relationship of the variables
					Bigger the MLE, the better the probability of our model being correct
					MLE tries to maximize the likelihood function
					When it can no longer be improve, it stops
		Log-Likelihood
				almost always negative, and the bigger, the better
		LL-Null: Log Likelihood Null
				The log likelihood of a model which has no independent variables

Like the F-Test with Linear Regression, the equivalent for Logarithmic Regression compares a ratio of Log-Likelihood to the LL-Null
		This is called the {{ Log Likelihood Ratio P - Value }}, or LLR p-value
			It measures if our model is statistically different from the LL-Null, a.k.a., a useless model with no explanatory power
			Just like Linear R. p - values, we want lower, and 0.000 is significant

Pseudo R-Squared
		a.k.a., AIC, BIC, and McFadden's R-Squared { what we are using }
			according to McFadden himself, a good pseudo r-squared is between 0.2 and 0.4


```
===========================================================================
                 coef    std err          z      P>|z|      [0.025      0.975]
---------------------------------------------------------------------------
const        -69.9128     15.737     -4.443      0.000    -100.756     -39.070
SAT            0.0420      0.009      4.454      0.000       0.024       0.060
===========================================================================
```

The Coefficient's Table ; Interpretation:
		Our Logit Model: $\log(\frac{\pi}{1 - \pi}) = -69.91 + 0.04 x SAT$
		the coefficient of the SAT is 0.0420,  and the multiplier of the constant {{ 1 }} is -69.9128, so the equation {{ where the variable portion of the equation is conveniently in linear form }} is: -69.91 + 0.04 x SAT
		$\pi$ is the odds of the event occurring and $1 - \pi$ is the odds of the event *not* occurring
				explicitly simplified:
				take the scenario where the input data is two SAT scores. The model would create two equations, shown below:
						$\log(odds_2) = -69.91 + 0.04 x SAT_2$
						$\log(odds_1) = -69.91 + 0.04 x SAT_1$
					if we take the difference of these two equations, we get the following:
						 $\log(odds_2) = -69.91 + 0.042 x SAT_2$
				    -  $\log(odds_1) = -69.91 + 0.042 x SAT_1$ 
				   ------------------------------------
				       $\log(odds_2) - \log(odds_1) = 0.042 x( SAT_2 - SAT_1 )$
				   Then, we use the quotient rule for logs ; the difference of two logs is equal to the log of quotient of their arguments:
					   $\log(\frac{odds_2}{odds_1}) = 0.042 x( SAT_2 - SAT_1 )$
					Now, imagine the difference in SAT scores is 1 ; or one unit of SAT
						$\log(\frac{odds_2}{odds_1}) = 0.042$
					Put each side as an exponent to e because $\epsilon^{\log(x)} = x$
						 $\frac{odds_2}{odds_1} = \epsilon^{0.042}$
						 $\frac{odds_2}{odds_1} = 1.042$
					multiply each side by $odds_1$
							$odds_2 = 1.042 * odds_1$
						which can be read as:
								$odds_2 = 104.2 \% * odds_1$
								' $odds_2$ is 104.2% of $odds_1$, or 4.2% more likely than $odds_1$ '
								' also akin to as the rise of SAT scores increases by one, the odds of admittance increase by 4.2%
								$\Delta odds = \epsilon^{b_k}$
								the change in odds of a variable are equal to the exponent of that variable _k
						-
						**if it were an increase of 10**
							$\log(\frac{odds_2}{odds_1}) = 0.042 x( SAT_2 - SAT_1 )$
							$\log(\frac{odds_2}{odds_1}) = 0.042 x 10$
							$\log(\frac{odds_2}{odds_1}) = 0.42$
							$\epsilon^{\log(\frac{odds_2}{odds_1})} = \epsilon^{0.42}$
							$\frac{odds_2}{odds_1} = 1.522$
							$odds_2 = 1.522 * odds_1$ or
							$odds_2 = 152.2\% * odds_1$
									$odds_2$ are 152 % more likely than $odds_1$
						if it were an increase of 100
							$odds_2 = 66.69 * odds_1$ or 
							$odds_2 = 6669\% * odds_1$ 
									$odds_2$ are 6668% more likely than $odds_1$  | 66 times higher odds