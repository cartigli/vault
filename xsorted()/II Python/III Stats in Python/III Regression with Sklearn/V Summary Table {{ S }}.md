{{ same script consecutively built on }}
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

p_values = f_regression(x,y)[1]
print('\n','P - values from f_regression:','\n',p_values)

p_values.round(7)
print('\n','P - values rounded:','\n',p_values.round(7))

# define summary table size
#reg_summary = pd.DataFrame(data=['SAT','Rand 1,2,3'], columns=['Features'])
#print('\n',reg_summary)
# returns simple data frame only of the names of the features

#print(x.columns.values) = ['SAT','Rand 1,2,3']
reg_summary = pd.DataFrame(data=x.columns.values, columns=['Features'])
print('\n',reg_summary)

# add coefficients:
reg_summary['Coefficients'] = reg.coef_
print('\n',reg_summary)

# add p - values
print('\n','Final Summary Table with coef\'s and p - values:')
reg_summary['P - values'] = p_values.round(5)
print(reg_summary)