Regression with Standardized Data allows us to better evaluate the impact each variable has on the dependent - scaled for relative impacts of independent variables
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
sns.set()
from sklearn.linear_model import LinearRegression

data = pd.read_csv('/Volumes/HomeXx/compuir/Downloads/1.02. Multiple linear regression.csv')

# declare variables
x=data[['SAT','Rand 1,2,3']]
y=data['GPA']

# import the sklearn standardization module
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler() # create empty StandardScalar object

# employ the scaling mechanism
scaler.fit(x) # calculates the mean and std dev for each feature

# apply the mechanism ; no longer an empty object
x_scaled = scaler.transform(x)

print(x_scaled[:5])

# regression with scaled features:
reg = LinearRegression()
reg.fit(x_scaled,y)

print('\n',reg.fit(x_scaled,y)) # only confirms input accepted

reg.coef_ # find new coefficient

reg.intercept_ # find y - intercept of the model

#reg_summary = pd.DataFrame(data=['Bias','SAT','Rand 1,2,3'], columns=['Features']) # MY METHOD
#reg_summary = pd.DataFrame(data=[['Intercept'],['SAT'],['Rand 1,2,3']], columns=['Features']) ** VIDEO'S METHOD
reg_summary = pd.DataFrame(data=[['Bias'],['SAT'],['Rand 1,2,3']], columns=['Features']) # VIDEO'S METHOD - and changed intercept to ' bias '
# this like laying out the blueprint for your summary table ^
# using [ ] for every item makes a 2D array of lists ; more specific and better for adding columns in the future

#reg_summary['Coefficients']=reg.coef_
# reg_summary['Y - Intercept']=reg.intercept_ { moved to og dataframe }
reg_summary['Weights'] = reg.intercept_, reg.coef_[0], reg.coef_[1]
# this is filling in the important values from calculations ^
# bigger the weight, bigger the impact
# smaller the weight, less significant the contribution to the model
# standardization allows us to see this impact effectively and more common than p - values for ML ; why sklearn doesn't do p - value calculations

print('\n',reg_summary)