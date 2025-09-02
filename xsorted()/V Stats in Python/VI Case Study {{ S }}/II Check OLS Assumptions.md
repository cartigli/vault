removed comments ofc, and graphs of var's & extraneous print comments on data's contents & current state
ran multicollinearity test against the features & decided to remove year
```python
import numpy as np
import pandas as pd
import statsmodels.api as sm
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.linear_model import LinearRegression
sns.set()

raw_data = pd.read_csv('/Volumes/HomeXx/compuir/1.04. Real-life example.csv')

print('\n','Columns labels:','\n',raw_data.columns) # info was cutoff
# we have Brand, Price, Body, Mileage, Engine V, Engine Type, Registration, Year, & Model ; we want to predict Price

# drop Model using Pandas using pandas' .drop() method
data = raw_data.drop(['Model'],axis=1)

# find empty values or missing data
data.isnull()

# true = 1 and false = 0, so the method below can count missing values
data.isnull().sum() # add all 'True's' together

# remove entries with missing values
data_no_mv = data.dropna(axis=0)
#print(data_no_mv.describe(include='all'))

# pandas' DataFrame.quantile() method 
q = data_no_mv['Price'].quantile(0.99) # take bottom 99% from Prices
data_1 = data_no_mv[data_no_mv['Price']<q]

# repeat process for Mileage
q = data_1['Mileage'].quantile(0.99)
data_2 = data_1[data_1['Mileage']<q] # take bottom 99% from Mileage

# use data 2 to continue with creatoin of cleaned data
data_3 = data_2[data_2['EngineV']<6.5] # hardcoded rather than quantile

# we'll do the same as Mileage but top 99%
q = data_3['Year'].quantile(0.01)
data_4 = data_3[data_3['Year']>q] # data_4 is Year's values above 1%

# finally, set the new cleaned data to a new variable: cleaned_data
data_cleaned = data_4.reset_index(drop=True)

# check the final cleaned data
data_cleaned.describe(include='all')



# Check OLS Assumptions
# make a scatter plot for continuous variables against the Price
f, (ax1, ax2, ax3) = plt.subplots(1, 3, sharey=True, figsize=(13,3))

# year vs price scatter plot ; looked exponentially positive
ax1.scatter(data_cleaned['Year'],data_cleaned['Price'])
ax1.set_title('Price & Year')

# engine v vs price scatter plot ; looked fairly linear , but clustered
ax2.scatter(data_cleaned['EngineV'],data_cleaned['Price'])
ax2.set_title('Price & Engine V[olume]')

# mileage vs year scatter plot ; looked exponentially negative
ax3.scatter(data_cleaned['Mileage'],data_cleaned['Price'])
ax3.set_title('Price & Mileage')

plt.show()
plt.close()

# we know price's scatter plot is not linear, so it could not have a linear relationship with its variables
# we will have to transform one or more to perform a regressional analysis
# log transformation is helpful for correcting exponentiality
# np.log(x) returns the natural logarithm of a number or array of numbers
log_price = np.log(data_cleaned['Price'])
data_cleaned['log_price'] = log_price # add new values as column to data
print(data_cleaned.columns)
print('\n',data_cleaned.head()) # yup, it was added!

# Check OLS Assumptions against Log_Price
# make a scatter plot for continuous variables against the Price
f, (ax1, ax2, ax3) = plt.subplots(1, 3, sharey=True, figsize=(13,3))

# year vs log_price scatter plot ; looked exponentially positive
ax1.scatter(data_cleaned['Year'],data_cleaned['log_price'])
ax1.set_title('Price & Year')

# engine v vs log_price scatter plot ; looked fairly linear , but clustered
ax2.scatter(data_cleaned['EngineV'],data_cleaned['log_price'])
ax2.set_title('Price & Engine V[olume]')

# mileage vs log_price scatter plot
ax3.scatter(data_cleaned['Mileage'],data_cleaned['log_price'])
ax3.set_title('Price & Mileage')

# the graphs show a substantially more linear relationship between price and the independent variables now

plt.show()
plt.close()

# drop the old Price as it is ' dirty '
data_cleaned = data_cleaned.drop(['Price'],axis=1)

# multicollinearity
# mileage and years could correlate ; and so should be cause for concern and check
# variance inflation factor {{ VIF }} is good for this
# produces a measure estimating how much largere the sqr root of the std error is compared to a situation where the variable is completely uncorrelated

from statsmodels.stats.outliers_influence import variance_inflation_factor
variables = data_cleaned[['Mileage','Year','EngineV']] # define features to check for multicollinearity
vif = pd.DataFrame()
vif["VIF"] = [variance_inflation_factor(variables.values, i) for i in range(variables.shape[1])]
vif["features"] = variables.columns

# vif can be 1 - inf
# if vif = 1 ; there is no multicollinearity
# if vif is over 5, probably multicollinearity exists
# ranges from person to person, sometimes 6 or 7 is the cutoff
# from our test here, only year possessed a significant VIF {{ over 10 }}
# engine V was over 7, but we'll ignore for now
print(vif)

data_no_multicollinearity = data_cleaned.drop(['Year'], axis=1) # drop the whole columns 
print(data_no_multicollinearity.columns)
print(data_no_multicollinearity.head())