```python
# import relevant libraries
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import statsmodels.api as sm # for running regressions

# load the data (from .csv file)
#data = pd.read_csv('1.01.+Simple+linear+regression.csv')
data = pd.read_csv(r'C:\Users\carto\vault\TheVault\udemy\II Py\IV Statistics in Py\1.01.+Simple+linear+regression.csv')
# data =... loads the csv data into a data frame
print(data) # {{responds with table pulled from the .csv file}}
# outputs the data frame defined above; columns SAT & GPA

# data.describe() offers more descriptive statistics
print(data.describe()) # shows count, mean, stddev, max, min, etc.,
# print() only needed for script format output in obsidian
# lets make a regression to describe the relationship between SAT's and resulting GPA's {{ from uni }}
# define dependent and independent variables
y = data['GPA'] # this regression looks to explain the relationship of GPA[dependent] depending on SAT[independent]
# we panda, we define the frame the variable originates from and assign it as dependent or independent; y or x
x1 = data['SAT'] # dependent variable

plt.scatter(x1,y) # make a scatter plot to demonstrate visually using matplotlib
plt.xlabel('SAT',fontsize=20) # label the axi
plt.ylabel('GPA',fontsize=20)
plt.show() # show scatter plot of x and y variables 

# on scatter plot, we can see trend pointing positively to the top-right of the graph
# what's the actual regression?

x = sm.add_constant(x1) # us scikit-learn to add a constant variable to the regression equation we're building
results = sm.OLS(y,x).fit() # use the scik to return the Ordinary Least Squares regression to the equation
# fit() applies an estimation of best fit using the OLS method to obtain the fit of the model
# results.summary() will often privide the relavant info
results.summary() # shows, r, r^2, slope, etc.,
print(results.summary()) # script adaptation

plt.scatter(x1,y)
yhat = 0.0017*x1 + 0.275
fig = plt.plot(x1, yhat, lw=4, c='orange', label='regression line') # plot the line of best fit on the graph in orange
plt.xlabel('SAT',fontsize=20)
plt.ylabel('GPA',fontsize=20)
plt.show()
print(plt.show()) # script adaption
```