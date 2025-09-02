```python
import numpy as np
import pandas as pd
import statsmodels.api as sm
import matplotlib.pyplot as plt
import seaborn as sns
sns.set()

raw_data = pd.read_csv('/Volumes/HomeXx/compuir/2.02. Binary predictors.csv')

print(raw_data.head()) # contains third gender value

# map both binary values to 1's & 0's
data = raw_data.copy()

data['Admitted'] = data['Admitted'].map({'Yes':1,'No':0})
data['Gender'] = data['Gender'].map({'Female':1,'Male':0})

print('\n',data.head(),'\n')


#declare the independent and dependent variables
y = data['Admitted'] # dependent variable
#x1 = data['Gender'] # independent variable
x1 = data[['SAT','Gender']]
#x1 = data['SAT']

# regression
x = sm.add_constant(x1)
reg_log = sm.Logit(y,x)
results_log = reg_log.fit()
print(results_log.summary())


np.set_printoptions(formatter={'float': lambda x: "{0:0.2f}".format(x)})


print(results_log.predict()) # outputs the predicted values ; all are 0 - 1
# we have the correct predictions for the model in data['Admitted']
print(np.array(data['Admitted']))

# now use sm's .LogitResults.pred_table() - returns a table which compares predicted and actual values
print(results_log.pred_table()) # this returns the confusion matrix
# comparison of predictions {{ results)log.predict() }} and actual {{ data['Admitted'] }} 

# beautify the confusion matric {{ cm }} with a pandas DataFrame {{ df }}
cm_df = pd.DataFrame(results_log.pred_table())
cm_df.columns = ['Predicted 0','Predicted 1']
cm_df = cm_df.rename(index={0:'Actual 0',1:'Actual 1'})
print(cm_df)

# formula for percentage accuracy
cm = np.array(cm_df)
#cm[0,0] this is like row 0, pos 0
#cm[1,1] this is like row 1, pos 1
# together they specify the correct values from the cm
# to get percent, we add them together and divide by the whole
perc = (cm[0,0] + cm[1,1]) / cm.sum()
print(perc)



# testing the model ; load the testing dataset
test = pd.read_csv('/Volumes/HomeXx/compuir/2.03. Test dataset.csv')

# map the same key value pairs to 1's and 0's
test['Admitted'] = test['Admitted'].map({'Yes':1,'No':0})
test['Gender'] = test['Gender'].map({'Female':1,'Male':0})


# make predictions with the model using the test data
# generate a new confusion matrix


test_actual = test['Admitted'] # actual outcomes we observed
test_data = test.drop(['Admitted'],axis=1) # everything but outcome

test_data = sm.add_constant(test_data)

#print(test_data) # got lucky variables were in order without req reordering

def confusion_matrix(data, actual_values, model): # where's model defined?
	pred_values = model.predict(data) # model is given, not defined, by the input variables {{ cm = confusion... line }}
	# results_log = reg_log.fit(x,y) <- our model
	# the input data {{ test and actual }} should be frames or arrays in the same shape as the training data {{ we tested this }}
	# { below } make a bin for values
	bins = np.array([0, 0.5, 1])
	# make a numpy histogram where values between 0 and 0.5 are considered 0, and values between 0.5 and 1 are considered 1
	cm = np.histogram2d(actual_values, pred_values, bins=bins)[0]
	# calculate accuracy - same formula from previous calculation
	accuracy = (cm[0,0] + cm[1,1]) / cm.sum()
	# return derived values
	return cm, accuracy

cm = confusion_matrix(test_data, test_actual, results_log)

print(cm)

# instead of raw confusion matrix, can beautify again
cm_df = pd.DataFrame(cm[0]) # two lines above, we define cm as a tuple, and the confusion_matrix fx returns a ( cm, accuracy ) tuple. by specifying the index of [0] , or the first item , we get the cm matrix 
cm_df.columns = ['Predicted 0', 'Predicted 1']
cm_df = cm_df.rename(index={0:'Actual 0',1:'Actual 1'})
print(cm_df)