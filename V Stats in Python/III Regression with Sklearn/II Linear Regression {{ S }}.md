 first regression with sklearn example
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
sns.set()

from sklearn.linear_model import LinearRegression # new | import the linear model from sklearn instead of the statsmodels lib

data = pd.read_csv('C:/Users/carto/Downloads/1.01.+Simple+linear+regression.csv') # use panda to read data from csv sheet

print(data.head()) # will show the top 5 Elements
print('\n')

# variables
# we want predictions for GPA based on SAT scores, so SAT is input / independent variable // feature
# GPA is dependent / output variable
# prediciting GPA with a single feature; SAT's
# declare them as such
x = data['SAT'] # independent feature
y = data['GPA'] # dependent output / target

print('intial shape of variables from panda:')
print(x.shape) # check their dimensions
print(y.shape) # both are (84,) with the simple linear dataset
# (84,) = vectors of 84 length each
print('\n')

# modify the shapes (84,) to be 2D, like how sklearn expects
# x_matrix = x.values.reshape(84,1) # add dimension without modifying data
x_matrix = x.values.reshape(-1,1) # does the same thing but is more generalized and needs no specification for the number of values 
# let x_matrix be equal to the values of x reshaped to be in the shape (84,1)
print('Modified input data shape:')
print(x_matrix.shape) # check the dimensional transformation was applied
print('\n')

# regression
reg = LinearRegression() # reg is now an instance of the LinearRegression class
# need elaboration on this
reg.fit(x_matrix,y) # x_matrix = input ; y = target ; order is crucial
# responds with LinearRegression() meaning model spun up

# to find the r^2 found:
reg.score(x_matrix,y) # outputs .4062384823...
print('R-squared:')
print(reg.score(x_matrix,y))
print('\n')

# coefficients:
reg.coef_
print('Reg.coef:')
print(reg.coef_) # outputs nd arrar containing all coef's { says array in terminal }
# in this case, it was one coef for the one feature in our model ; the constant is insignificantly dif than 0
print('\n')

# y - intercept
print('Intercept:')
reg.intercept_
print(reg.intercept_) # float value
print('\n')

# prediction
print('Prediction{s}:')
# the video's syntaxign is outdated, below is the proper notation
reg.predict([[1750]])
print(reg.predict([[1750]])) # outputs array of one dimension
print('\n')

# can also use panda for a DataFrame
# make a dataframe of two inputs for predictions of the model
new_data = pd.DataFrame(data={1750,1650},columns=['SAT'])
print(new_data)
print('\n')

# predict on new_data
reg.predict([[new_data]])
print(reg.predict([new_data]))
print('\n')

# can add it to new_data as well
new_data['Predicted GPA'] = reg.predict(new_data)
print(new_data) # or just ' new_data ' if terminal
print('\n')

# and the regression model over the scatter plot
plt.scatter(x,y)
yhat = reg.coef_ * x_matrix + reg.intercept_
fig = plt.plot(x, yhat, lw=4, c='orange', label='regression line')

plt.xlabel('SAT', fontsize=20)
plt.ylabel('GPA', fontsize=20)

plt.show()