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

reg_summary = pd.DataFrame(data=[['Bias'],['SAT'],['Rand 1,2,3']], columns=['Features']) # VIDEO'S METHOD - and changed intercept to ' bias '
# this like laying out the blueprint for your summary table ^
# using [ ] for every item makes a 2D array of lists ; more specific and better for adding columns in the future

reg_summary['Weights'] = reg.intercept_, reg.coef_[0], reg.coef_[1]
# this is filling in the important values from calculations ^
print('\n',reg_summary)

new_data = pd.DataFrame(data=[[1700,2],[1800,1]],columns=['SAT','Rand 1,2,3']) # test values are same shape as input variables ; 1 & 2 are values for [ Rand 1,2,3 ]
print('\n','test data shape:',new_data.shape) # 2 sets of 2 columns
print('input data shape:',x_scaled.shape) # input data was 84 sets of 2 columns
print('\n','new summary table { no values }:','\n',new_data)

# perform prediction
prediction = reg.predict(new_data)
print('\n','Predictions on unscaled data:','\n',prediction) # gives weird values of 295.4, 312.6 because unstandardized ! need to standardize over the mean and standard deviation of the ' training data '
# this info is stored in the scaled object from earlier
new_data_scaled = scaler.transform(new_data)
print('\n','New scaled data:','\n',new_data_scaled) # outputs nd array of four values ; one per input which was the shape of 2 rows by 2 columns ; 4 !

# predict with transformed and normalized test points:
new_predictions = reg.predict(new_data_scaled)
print('\n','Scaled input predictions:','\n',new_predictions)




# new method ; removes rand 123 for regression
reg_simple = LinearRegression()
x_matrix_slice = x_scaled[:,0]
x_matrix_simple = x_matrix_slice.reshape(-1,1)
#x_simple_matrix = x_scaled[:,0].reshape(-1,1)
# make a new simple matrix for only the SAT scores, [:,0] means slice all rows, but only the first column {{ (84,2) becomes (84,1) }} and reshape by ( -1 , 1 )

# before and after slicing/reshaping:
print('\n','x_scaled before slice and reshape:')
print(x_scaled.shape,'\n')
print('x_scaled after slicing:')
print(x_matrix_slice.shape,'\n')
print('x_scaled after reshaping:')
print(x_simple_matrix.shape,'\n')

reg_simple.fit(x_simple_matrix,y) # perform the calculations ; make the model

# make the prediction on new_data_scaled after slicing & reshaping
# just like the training data
simple_prediction = reg_simple.predict(new_data_scaled[:,0].reshape(-1,1))
print('New prediction on only SAT\'s & scaled:')
print(simple_prediction)

print('\n','Compare to the predictions with rand 123:','\n',new_predictions)

print('\n','The similarity confirms the rand 123 variables did not impact the model\'s explanatory power; it is insignificantly different from 0. This is also why Sklearn does not have built in functions for p-values; there are other more reliable methods for determining the effect a variable has on the model.')

#simple_predict = reg_simple.predict(new_data_scaled[:,0]) DIDNT RESHAPE TEST DATA