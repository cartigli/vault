```python
import numpy as np # numbers
import pandas as pd # data
import matplotlib.pyplot as plt # math
import statsmodels.api as sm # graphs
import seaborn # fancy
seaborn.set() # fancy graphs

data = pd.read_csv('C:/Users/carto/downloads/1.02.+Multiple+linear+regression.csv')

print(data)
print(data.describe())

y = data['GPA'] # still same y-hat for predicition
x1 = data[['SAT','Rand 1,2,3']] # data frame containing two series

x = sm.add_constant(x1)
results = sm.OLS(y,x).fit()

print(results.summary())
```

===============================================
                 coef         std err         t           P>|t|      [0.025      0.975]
----------------------------------------------------------------------------
const          0.2960      0.417      0.710      0.480      -0.533       1.125
SAT            0.0017      0.000      7.432      0.000       0.001       0.002
Rand 1,2,3  -0.0083      0.027     -0.304      0.762      -0.062       0.046

this was output; the r^2 increased but the adjusted, decreased; we gained a variable but lost value or accuracy with our model
	also, rand was negatively effective; p-value of 0.8 suggests insignificance - this variable worsened the model

$R^2$ & $R^2 Adjusted$ are only ever relevant when comparing two models with the same dependent variable {{ $y$ }} and the same dataset