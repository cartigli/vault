'/Volumes/HomeXx/compuir/xsell/data_proc.csv'
```python
import numpy as np
import pandas as pd
from sklearn import metrics
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split
import pickle

# preprocessed
data = pd.read_csv('/Volumes/HomeXx/compuir/xsell/data_proc.csv')

processed = data.copy()

pd.options.display.max_columns = None # max columns


# try to predict if they are above average absent or below
# base it on current median of dataset's absenteeism time in hours

median = processed['Absenteeism Time in Hours'].median()
print(median) # returned 3.0 , so if someone has been over 3 hours absent, this is excessive
# we change the values of time of absenteeism to 0 for those below 3 and 1 for those above
# this way we can train the model to predict whether they are over the mean

# np.where(condition, val1, val2) checks if a condition has been satisfied, value if true, value if false
targets = np.where(processed['Absenteeism Time in Hours'] > median, 1, 0)
print(targets[0]) # arrays of 1's and 0's

processed['Excessive Absenteeism'] = targets
#print(processed.head())
print(processed.columns.values)

# check the split 
e_ratio = targets.sum() / targets.shape[0]
print(f"E_ratio:{e_ratio}") # about 45% are 1's, ~ 55% are 0's

proctargets = processed.drop(['Absenteeism Time in Hours'], axis=1) # drop column
print(proctargets.columns.values)


# select inputs for regression
unscaled_inputs = proctargets.iloc[:,:14]

# scale inputs
scaler = StandardScaler()
scaler.fit(unscaled_inputs) # prepare mechanism
scaled_in = scaler.transform(unscaled_inputs)

print(scaled_in,scaled_in.shape)


# split t v t 
xtrain, xtest, ytrain, ytest = train_test_split(scaled_in, targets, train_size=0.8, shuffle=True, random_state=222)

print(xtrain.shape, xtest.shape, ytrain.shape, ytest.shape) #(560,14),(140,14),(560,),(140,)

reg = LogisticRegression()
print(reg.fit(xtrain, ytrain)) # make the model

print(reg.score(xtrain, ytrain)) # got like 77%

print(reg.intercept_)
print(reg.coef_)

#reg.predict(xtest,ytest)
print(reg.score(xtest,ytest))

# or get probabilities
proba_test = reg.predict_proba(xtest)
p_test = reg.predict(xtest)
print(proba_test) # shows probability of 0 in column 1 and probability of getting 1 in the second column


# save the model
# reg() holds the model's value's and its predictive power
# pickle[module]
# with open(filename, 'write-bytes') as file:
#    pickle.dump = save - reg
with open('model', 'wb') as file:
	pickle.dump(reg, file)

# scaler needs to be saved as well becuase if someone else wants to use this model, their data will need to be scaled in the same way

with open('scaler','wb') as file:
	pickle.dump(scaler, file)