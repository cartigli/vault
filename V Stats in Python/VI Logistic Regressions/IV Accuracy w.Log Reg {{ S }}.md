```python
import numpy as np
import pandas as pd
import statsmodels.api as sm
import matplotlib.pyplot as plt
import seaborn as sns
sns.set()

raw_data = pd.read_csv('C:/Users/carto/2.02.+Binary+predictors.csv')

print(raw_data.head()) # contains third gender value

# map both binary values to 1's & 0's
data = raw_data.copy()

data['Admitted'] = data['Admitted'].map({'Yes':1,'No':0})
data['Gender'] = data['Gender'].map({'Female':1,'Male':0})

print('\n',data.head(),'\n')


#declare the independent and dependent variables
y = data['Admitted'] # dependent variable
#x1 = data['Gender'] # independent variable
#x1 = data[['SAT','Gender']]
x1 = data['SAT']

# regression
x = sm.add_constant(x1)
reg_log = sm.Logit(y,x)
results_log = reg_log.fit()
print(results_log.summary())

results_log.predict() # outputs the predicted values ; all are 0 - 1
# we have the correct predictions for the model in data['Admitted']
np.array(data['Admitted'])

# now use sm's .LogitResults.pred_table() - returns a table which compares predicted and actual values
print(results_log.pred_table()) # this returns the confusion matrix
# [[69.  5.]
# [ 4. 90.]] {{ this shows how confused the model is }}
# it is read as:
#           Predicted 0  |  Predicted 1
# Actual 0:    69.             5.
# Actual 1:     4.            90.
# top right: The model predicted 0 when the outcome was actually 0
# bottom left: The model predicted 1 when the outcome was actually 1
# these are correct
# for four of the model's prediction of 0 the outcome was actually 1, and vice versa, which were incorrect predictions
# the model got 159 / 168 , or 95 % accuracy
#
# if only gender is used as a variable, the confusion matrix is:
# [[59. 15.]
# [31. 63.]]
# the model correctly predicted 122 / 168 , or 73 % accuracy
#
# if only SAT scores are input as a variable:
# [[67.  7.]
# [ 7. 87.]]
# this model predicted 154 of 168 , or 92 % accuracy