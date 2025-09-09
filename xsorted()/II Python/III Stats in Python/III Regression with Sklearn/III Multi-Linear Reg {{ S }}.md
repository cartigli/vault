```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import statsmodels.api as sm
import seaborn as sns
sns.set()

from sklearn.linear_model import LinearRegression

# load the data
data = pd.read_csv('/Volumes/HomeXx/compuir/Downloads/1.02. Multiple linear regression.csv')
print(data.head()) # shows SAT, RAND123, and GPA columns
# two input features; SAT & RAND123

# declare variables independent and dependent 
x=data[['SAT','Rand 1,2,3']] # data frame for multiple var's
y=data['GPA']

# regression
reg = LinearRegression()
reg.fit(x,y) # prints ' LinearRegression() '
print('\n',reg.fit(x,y)) # for scripts

reg.coef_ # coefficient ; array of two values ; model's slope
print('\n','coefficients:',reg.coef_)
# ceofficients of SAT & Rand 1,2,3

reg.intercept_ # y - intercept of model ; returns float
print('\n','y - intercept:',reg.intercept_)

# ' goodness of fit '
# reg.score(x,y) returns the r-squared of a linear regression
reg.score(x,y) # not adjusted r - squared !
print('\n','R - squared:',reg.score(x,y))

# adjusted r - squared which penalizes extraneous variables
# sklearn has no such fx ; we'll make our own calculation

# adjusted r - squared manual calculation:
#$R^2_{adj.} = 1 - ( 1 - R^2 ) * \frac{ n - 1 }{ n - p - 1 }$
# ^ latex cmd syntaxxing
x.shape # returns (84,2) 2 dimensions, 84 x 2 shape
# 84 predicitions ; 2 predictors
#r_adj = 1 - ( 1 - reg.score(x,y)) * ((84 - 1)/(84 - 2 - 1))
#print('\n','R - adjusted:',r_adj)

# improved adjusted r - squared calculation:
# x.shape[0] is the first dimension ; 84
# x.shape[1] is the second dimension ; 2
#r_adj = 1 - ( 1 - reg.score(x,y)) * ((x.shape[0] - 1)/(x.shape[0] - x.shape[1] - 1))
#print('\n','R - adjusted:',r_adj)

# further improved:
r2 = reg.score(x,y)
n = x.shape[0] # first dimension of x
p = x.shape[1] # second dimension of x

r_adj = 1 - ( 1 - r2 ) * (( n - 1) / ( n - p - 1 ))
print('\n','R - adjusted:',r_adj)


print('\n\n','COMPARE TO STATSMODELS.APIS CALCULATIONS:','\n')
# comapre to previous statsmodels calculations / results:
y = data['GPA'] # still same y-hat for predicition
x1 = data[['SAT','Rand 1,2,3']] # data frame containing two series

x = sm.add_constant(x1)
results = sm.OLS(y,x).fit()

print(results.summary())

```


$R^2_{adj.} = 1 - ( 1 - R^2 ) * \frac{ n - 1 }{ n - p - 1 }$