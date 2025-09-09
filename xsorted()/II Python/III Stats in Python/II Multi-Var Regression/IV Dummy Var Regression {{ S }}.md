Imitation, substitute for categorical data; Gender, Season, Brand
```python
import numpy as np
import pandas as pd
import statsmodels.api as sm
import matplotlib.pyplot as plt
import seaborn as sns
sns.set()

raw_data = pd.read_csv('C:/Users/carto/Downloads/1.03.+Dummies.csv') # unpack the dummies csv data into raw_data variable

#print(raw_data) # contains SAT, GPA, & new attendance var
# normally, we'd transform the yes & no's to ones and zeros; no = 0 and yes = 1

data = raw_data.copy() # create a copy of the raw_data and name it data
data['Attendance'] = data['Attendance'].map({'Yes':1,'No':0})
# set the variable Attendance from data {{ raw_data }} to be equal to the Attendance value mapped for 'Yes' = 1 and 'No' = 0 || in the pandas syntax
#print(data) # Yes' and No's are now 1's and 0's
#print(data.describe()) # descriptive stats of new data

# regression
y = data['GPA']
x1 = data[['SAT','Attendance']]

x = sm.add_constant(x1)
results = sm.OLS(y,x).fit()
print(results.summary())

# plot regression
print('\noriginal graph and scatter plot')
plt.scatter(data['SAT'],y) # original, all points uni-colored
yhat_no = 0.6439 + 0.0014*data['SAT']
yhat_yes = 0.8665 + 0.0014*data['SAT'] # if dummy variable is one, or yes, then it is counted as a constant and added to the model, so there are two slopes for each value for the dummy variable
fig = plt.plot(data['SAT'],yhat_no, lw=2, c='#006837') # show yhat_no in green
fig = plt.plot(data['SAT'],yhat_yes, lw=2, c='#a50026') # show yhat_yes in red
plt.xlabel('SAT',fontsize=20)
plt.ylabel('GPA',fontsize=20)
plt.show()

# regression with colored points on the scatter plot for each of their values of the dummy variable; red for yes/1, and red for no/0
print('\nimproved graph with colored scatter points')
# plot regression
# plt.scatter(data['SAT'],y) # original, all points uni-colored
plt.scatter(data['SAT'],y,c=data['Attendance'],cmap='RdYlGn_r') # alternate scatter plot that shows the dummy values as green and red depending on their value
yhat_no = 0.6439 + 0.0014*data['SAT']
yhat_yes = 0.8665 + 0.0014*data['SAT']
fig = plt.plot(data['SAT'],yhat_no, lw=2, c='#006837') # show yhat_no in green
fig = plt.plot(data['SAT'],yhat_yes, lw=2, c='#a50026') # show yhat_yes in red
plt.xlabel('SAT',fontsize=20)
plt.ylabel('GPA',fontsize=20)
plt.show()

# third scatter plot with regression
print('\nwith the original y_hat regression')
plt.scatter(data['SAT'],y,c=data['Attendance'],cmap='RdYlGn_r') # alternate scatter plot that shows the dummy values as green and red depending on their value
yhat_no = 0.6439 + 0.0014*data['SAT']
yhat_yes = 0.8665 + 0.0014*data['SAT']
yhat = 0.0017*data['SAT'] + 0.275
fig = plt.plot(data['SAT'],yhat_no, lw=2, c='#006837', label='regression line 1') # show yhat_no in green
fig = plt.plot(data['SAT'],yhat_yes, lw=2, c='#a50026', label='regression line 2') # show yhat_yes in red
fig = plt.plot(data['SAT'],yhat, lw=3, c='#4C7280', label='regression line') # og yhat in blue
plt.xlabel('SAT',fontsize=20)
plt.ylabel('GPA',fontsize=20)
plt.show()
```




```




output:
=============================================================
                 coef    std err          t      P>|t|      [0.025      0.975]
------------------------------------------------------------------------------
const          0.6439      0.358      1.797      0.076      -0.069       1.357
SAT            0.0014      0.000      7.141      0.000       0.001       0.002
Attendance     0.2226      0.041      5.451      0.000       0.141       0.304
```
the additional variable creates the new equation: 
			y = 0.6439 + 0.0014 * SAT + 0.2226 * Dummy Var
					all variables but the constant have significant p-values
