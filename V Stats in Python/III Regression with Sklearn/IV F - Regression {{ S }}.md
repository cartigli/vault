We know from the previous script and resulting regression that the additional variable decreased explanatory power 
we determine which variable through [Feature Selection with F - Regression]
			simplifies models, improves efficiency
			no built in method, but can work around
			F - Regressoin creates simple linear regressions of each feature and the ind var
						calculates regressions for each feature on the dependent variable [SAT, Rand 1,2,3]
this code will be stacked on the previous script with the comments stripped:
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import statsmodels.api as sm
import seaborn as sns
sns.set()

from sklearn.linear_model import LinearRegression

data = pd.read_csv('/Volumes/HomeXx/compuir/Downloads/1.02. Multiple linear regression.csv')
print(data.head()) # shows SAT, RAND123, and GPA columns


x=data[['SAT','Rand 1,2,3']] # data frame for multiple var's
y=data['GPA']

reg = LinearRegression()
reg.fit(x,y) # prints ' LinearRegression() '
print('\n',reg.fit(x,y)) # for scripts

reg.coef_ # coefficient ; array of two values ; model's slope
print('\n','coefficients:',reg.coef_)

reg.intercept_ # y - intercept of model ; returns float
print('\n','y - intercept:',reg.intercept_)

reg.score(x,y) # not adjusted r - squared !
print('\n','R - squared:',reg.score(x,y))

# further improved:
r2 = reg.score(x,y)
n = x.shape[0] # first dimension of x
p = x.shape[1] # second dimension of x

r_adj = 1 - ( 1 - r2 ) * (( n - 1) / ( n - p - 1 ))
print('\n','R - adjusted:',r_adj)

from sklearn.feature_selection import f_regression
print('\n','Feature f_regression:','\n',f_regression(x,y))
# outputs two arrays : the first is the f - statstic for each var
# the second is the corresponding p - values
# p - values are key, so let's distinguish them
p_values = f_regression(x,y)[1]
print('\n','P - values from f_regression:','\n',p_values)
# default to scientific notations ; rounding helps clarity
p_values.round(7)
print('\n','P - values rounded:','\n',p_values.round(7))
# first value is p - value of the SAT variable
# second is the p - value of the Rand 1,2,3 variable
# although simplistic, in linear models this allows us to determine usefulness of a variable; high p - values denote uselessness
