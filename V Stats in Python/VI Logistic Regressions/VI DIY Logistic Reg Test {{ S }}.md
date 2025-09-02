```python
import numpy as np
import pandas as pd
import statsmodels.api as sm
import matplotlib.pyplot as plt
import seaborn as sns
#from sklearn.preprocessing import train_test_split
#from sklearn.mdoel_selection import 

raw_data = pd.read_csv('/Volumes/HomeXx/compuir/Bank-data.csv')

print(raw_data)

data = raw_data.copy()

data['y'] = data['y'].map({'yes':1,'no':0})
print(data)

# define variables
y = data['y']
#x1 - data['duration']
# [[221. 38.] [ 82. 177.]] = cm of ^
#x1 = data[['duration','previous']]
# [[221. 38.] [ 82. 177.]] = cm of ^
#x1 = data[['duration','interest_rate']]
# [[204. 55.] [ 30. 229.]] = cm of ^
x1 = data[['duration','interest_rate','credit']]
# [[210. 49.] [ 29. 230.]] = cm of ^

x = sm.add_constant(x1)
reg_log = sm.Logit(y,x)
reg_results = reg_log.fit()

print(reg_results.summary())

print(reg_results.pred_table())

cm = reg_results.pred_table()
accuracy = (cm[0,0] + cm[1,1]) / cm.sum()
print('Training Accuracy in %:',accuracy)


# test the model
test_data = pd.read_csv('/Volumes/HomeXx/compuir/Bank-Data-Testing.csv')

test_data['y'] = test_data['y'].map({'yes':1,'no':0})

print(test_data.head())
y_hat = test_data['y']
x1 = test_data['duration']

x = sm.add_constant(x1)
reg_log = sm.Logit(y_hat,x)
reg_results = reg_log.fit()

print('Testing results:','\n',reg_results.summary(),'\n')

print('Testing cm:','\n',reg_results.pred_table())

cm = reg_results.pred_table()
accuracy = (cm[0,0] + cm[1,1]) / cm.sum()
print('Testing Accuracy in %:',accuracy)