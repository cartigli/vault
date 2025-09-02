How to test for significance of the model {{ F-Test }}

Like z, t distributions, the f-statistic follows a distribution, which is skewed right {{ leaning left }}
	statistic, so stems from a hypothesis test;
		$H_0 : \beta_1 = \beta_2 = \beta_3 . . . = 0$
				the null hypothesis is that all the beta coefficient values are equal to 0
				the $H_A$ is that at least one of the variables defers from 0; it explains some of the variability in y
					$H_A : at-least-one \beta_i \neq 0$

from [[II Multi-Variate Example {{ S }}]]
                            OLS Regression Results                            
==============================================================================
Dep. Variable:                    GPA   R-squared:                       0.407
Model:                            OLS   Adj. R-squared:                  0.392
Method:                 Least Squares   F-statistic:                     27.76
Date:                Thu, 28 Aug 2025   Prob (F-statistic):           6.58e-10
Time:                        22:38:00   Log-Likelihood:                 12.720
No. Observations:                  84   AIC:                            -19.44
Df Residuals:                      81   BIC:                            -12.15
Df Model:                           2                                         
Covariance Type:            nonrobust    
									*in the model above, we got an F-Statistic of 27.76, which was paired with a p-value of 6.58e-10; a very low number, and under 0.05, suggesting the model **is** relevant*
											however, this model's F-Statistic was lower, and p-value higher, than the single variate model's, so less accurate by another assessment