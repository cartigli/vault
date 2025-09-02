How to make predictions based on the regressions we create

```python
import numpy as np
import pandas as pd
import statsmodels.api as sm
import matplotlib.pyplot as plt
import seaborn as sns
sns.set()

raw_data = pd.read_csv('C:/Users/carto/Downloads/1.03.+Dummies.csv')
data = raw_data.copy()
data['Attendance'] = data['Attendance'].map({'Yes':1,'No':0})
#print(data) # Yes' and No's are now 1's and 0's
#print(data.describe()) # descriptive stats of new data

# regression
y = data['GPA']
x1 = data[['SAT','Attendance']]

x = sm.add_constant(x1)
results = sm.OLS(y,x).fit()
# print(results.summary())
# ^ OLS regression results

# scatter plot with regression
print('\nwith the original y_hat regression')
plt.scatter(data['SAT'],y,c=data['Attendance'],cmap='RdYlGn_r')
yhat_no = 0.6439 + 0.0014*data['SAT']
yhat_yes = 0.8665 + 0.0014*data['SAT']
yhat = 0.0017*data['SAT'] + 0.275
fig = plt.plot(data['SAT'],yhat_no, lw=2, c='#006837', label='regression line 1') # show yhat_no in green
fig = plt.plot(data['SAT'],yhat_yes, lw=2, c='#a50026', label='regression line 2') # show yhat_yes in red
fig = plt.plot(data['SAT'],yhat, lw=3, c='#4C7280', label='regression line') # og yhat in blue
plt.xlabel('SAT',fontsize=20)
plt.ylabel('GPA',fontsize=20)
plt.show()

# x is a data frame with three columns
#print(x) # triple check x is a data frame with three columns
# constant column/variable is multiplier for the x variable, and is equal to one

# make predicitions based on the model created/defined above:
# we will try to predict the GPA's of two students; one who got a 1700 on the SAT but attended less than 75% of their classes, and another who scores a 1670 on the SAT but attended 75% or more of their college courses
new_data = pd.DataFrame({'const':1,'SAT':[1700,1670],'Attendance':[0,1]})
# tends to be re-entered in alphabetical order, so rewrite the variable with defined columns
new_data = new_data[['const','SAT','Attendance']] # define new columns
# new new_data is 2 rows of 3 columns; two people and their related data
# name the rows their respective titles lol
#new_data.rename(index={0:'Bob',1:'Alice'}) # remap the indices of 0 and 1 {{ first and second element }} to key-value pairs containing their name
# ^ this did modify the new_data DataFrame, but didn't reassign the modified frame to the new_data variable
# corrected to reassign the modified DataFrame
new_data = new_data.rename(index={0:'Bob',1:'Alice'})
# check if modification was applied properly
print(' ')
print(new_data) # it was !

# prediction factory
# regression model was claddified under the variable results, so that is our tool for predicitions
# results = sm.OLS(x,y).fit()
predictions = results.predict(new_data) # this has one argument; new_data for Alice and Bob
print(' ')
print(predictions) # ensure the indexing was modified

predictionsdf = pd.DataFrame({'Predictions':predictions}) # transform predicitions into a DataFrame
joined = new_data.join(predictionsdf) # add a column of predictions for Bob and Alice to the new_data variable
# what's df?
#joined = joined.rename(index={0:'Bob',1:'Alice'}) # reapply indexing modification after joining the predictions and new_data DataFrame
# comenting out this line did not remove the Alice and Bob labels/columns so this line is redundant
# note that there are dozens of ways to do this
print(joined) # test new DataFrame