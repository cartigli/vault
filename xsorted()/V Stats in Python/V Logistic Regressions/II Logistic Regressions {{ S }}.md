A non-linear model; could be exponential, quadratic, or {{ Logistic }}
Implies the possible outcomes are not numerical, but rather categorical
		yes, or no
		0, or 1
		will they, or won't they

Linear Regression can predict how much someone will spend , *if they buy*
Logistic Regression can predict whether the customer will buy *at all* ; more fundamental predictions

instead of SAT -> GPA, with this logistic regression, we'll predict *whether or not they are accepted* based on SAT scores

```python
import numpy as np
import pandas as pd
import statsmodels.api as sm
import matplotlib.pyplot as plt
import seaborn as sns
sns.set()

raw_data = pd.read_csv('/Volumes/HomeXx/compuir/2.01. Admittance.csv')

print('Raw Data Frame:')
print(raw_data.head(),'\n') # contains admission status & SAT score

# admission status is notated with a yes or a no
# we need to modify this column to show yes's as 1's and no's as 0's
data = raw_data.copy() # create a copy of the dataset

# map Yes to 1 and No to 0 with Key-value Paring with .map({}) method
data['Admitted'] = data['Admitted'].map({'Yes':1,'No':0})

print('Data Frame Remapped:')
print(data.head(),'\n')

# set independent and dependent variables
y = data['Admitted'] # dependent variable
x1 = data['SAT'] # independent variable

# scatter plot variables
plt.scatter(x1,y)
plt.title('Scatter Plot for Initial Data Viewing')
plt.ylabel('Admmision Status', fontsize=10)
plt.xlabel('SAT', fontsize=10)
plt.show()
plt.close()
# ^ this is an almost useless scatter plot; all values are either 1 or 0
# a linear regression for this dataset would show a line at 45 degrees, going over and below the minimum and maximum points

print(' ')
print(' ')


# CREATE A LOGISTIC REGRESSION W/STATS_MODELS 

x = sm.add_constant(x1)

# declare a regression var; then a way to calculate it | .Logit() method
# .Logit() takes the independent and dependent variables as inputs
# note that this order above is not optional
reg_log = sm.Logit(y,x) # similar to OLS' but Logistical
results_log = reg_log.fit() # apply the fit to the model, and set the output equal to results_log

print('\n\n',results_log) # returned text returned below in comments:
#Optimization terminated successfulOptimization terminated successfully. Current function value: 0.137766 Iterations 10ly.
#         Current function value: 0.137766
#         Iterations 10
# This output means the following: the regression succesfuly occurred, the function went through 10 iterations of training, and 0.1377... is the ' objective function ' after the 10th iteration, which is similar to ' cost '
# stats models' limit on iterations is 35

# results summary
print('\n',results_log.summary())