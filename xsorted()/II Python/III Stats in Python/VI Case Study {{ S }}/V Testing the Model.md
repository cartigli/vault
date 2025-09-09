removed comments and prints, light re-working
```python
import numpy as np
import pandas as pd
import statsmodels.api as sm
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.linear_model import LinearRegression
from sklearn.preprocessing import StandardScaler
from sklearn.model_selection import train_test_split
sns.set()

raw_data = pd.read_csv('/Volumes/HomeXx/compuir/1.04. Real-life example.csv')

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

# **Check OLS Assumptions**

# we know price's scatter plot is not linear, so it could not have a linear relationship with its variables
log_price = np.log(data_cleaned['Price'])
data_cleaned['log_price'] = log_price # add new values as column to data

# drop the old Price as it is ' dirty '
data_cleaned = data_cleaned.drop(['Price'],axis=1)

# multicollinearity check on features ; {{ 1 / 1 - r-squared }}
from statsmodels.stats.outliers_influence import variance_inflation_factor
variables = data_cleaned[['Mileage','Year','EngineV']] # define features to check for multicollinearity
vif = pd.DataFrame()
vif["VIF"] = [variance_inflation_factor(variables.values, i) for i in range(variables.shape[1])]
vif["features"] = variables.columns

data_no_multicollinearity = data_cleaned.drop(['Year'], axis=1) # drop the whole columns 

# **adding dummies**

data_with_dummies = pd.get_dummies(data_no_multicollinearity, drop_first=True) # drop first for n - 1 dummies

# do a * very, very * manual adjustment to move the dependent var to the first pos
cols = ['log_price', 'Mileage', 'EngineV', 'Brand_BMW', 'Brand_Mercedes-Benz', 'Brand_Mitsubishi', 'Brand_Renault', 'Brand_Toyota', 'Brand_Volkswagen', 'Body_hatch', 'Body_other', 'Body_sedan', 'Body_vagon', 'Body_van', 'Engine Type_Gas', 'Engine Type_Other', 'Engine Type_Petrol', 'Registration_yes']
data_preprocessed = data_with_dummies[cols]


# **The Linear Regressoin Itself**


# define targets and variables:
targets = data_preprocessed['log_price'] # targets are the price { after log transformation }
inputs = data_preprocessed.drop(['log_price'],axis=1) # inputs = all but price


# scale the data
scaler = StandardScaler()
scaler.fit(inputs) # calculates scaling rates, mean, sigma, etc.,

inputs_scaled = scaler.transform(inputs) # apply the scaling

# complete a train & test split with train_test_split()
x_train, x_test, y_train, y_test = train_test_split(inputs_scaled, targets, test_size=0.2, random_state=365) # split train/test data 80/20 among inputs_scaled and targets so they are given to x_{train/test} and y_{train/test} respecitively


# create the regression
reg = LinearRegression() # initiate reg as an instance of LinearReg class
reg.fit(x_train, y_train) # create the regression on the split data
# note : this is a log regression due to the transformation we applied on price ; it is a Log-Linear Regression

y_hat = reg.predict(x_train) # check result by plotting predicted values against observations

# calculate the R^2
score = reg.score(x_train, y_train)
print('\n','R Squared:',score)

# find the weights and bias
print('\n','Intercept:',reg.intercept_)
print('^ Scalar')

print('\n','Coeff:','\n',reg.coef_)
print('^ Array of all features and consequently, dummy vars','\n')


# create a summary table with features corresponding to weights
reg_summary = pd.DataFrame(inputs.columns.values, columns=['Features'])
# add to the reg_summary table by introducing a new column; ' Weights '
reg_summary['Weights'] = reg.coef_ # set it equal the coefficients

print('Reg.Summary of dummy vars, vars, and their weights:','\n')
print(reg_summary)

# dummy vars
# we dropped category per unique variable, when all dummy vars are 0 and the dropped var is 1 ; look at brand for example
print('\nBrand count:')
print(data_cleaned['Brand'].unique()) # shows us all unique brands in the brand category {{ after cleaning data }}

print('\n',data_cleaned['Registration'].unique()) # returns yes & no



# Test the Model
y_hat_test = reg.predict(x_test) # store predicitions in y_hat_test and test on the x_test data split

# plot against targets and check for 45 degree line
plt.scatter(y_test, y_hat_test, alpha=0.2) # targets vs model's predicitions on test data
plt.xlabel('Targets (y_test)',size=10)
plt.ylabel('Predictions (y_hat_test)',size=10)
plt.xlim(6,13)
plt.ylim(6,13)
plt.show() 
plt.close()
# notes, higher prices = more accurate predictions
# coincidentally, lower prices = less accuracy
# plt.scatter(x,y[,alpha]) creates a scatter plot and [,alpha] specifies the opacity
# more concentrated points = increased opacity
# less concentrated points = increased translucincy
# shows accuracy better , or more clearly 

# data frame performance 
#df_pf = pd.DataFrame(y_hat_test, columns=['Prediction']) # dataframe on the predictions {{ y_hat_test }} only
#print('\n',df_pf.head()) # shows the log prices ; sub-optimal
# log is opp. of exp., so take the exp. of the prices
# np.exp(x) method returns the rxponential of x {{ or ' e ' to the power of x }}
#print(' ')
#np.exp(df_pf)
#print(np.exp(df_pf).head())
# instead of the inefficient method above, add it to the og dataframe

df_pf = pd.DataFrame(np.exp(y_hat_test), columns=['Prediction']) # dataframe on the predictions {{ y_hat_test }} only
print('\n',df_pf.head()) # shows predicitions as og Prices

# compare them to the targets, or t_test
y_test = y_test.reset_index(drop=True) # remove incorrect indi
df_pf['Target'] = np.exp(y_test)

print('\n','Predictions with Targets:')
print(df_pf.head())

# this failed to succesfuly compare them as the initial indices from the data split function persisted, and pandas tried to match them to the predictions, which casues Nan values
# we need to override the original indices and forget them
# to this with the .reset_index() method with drop=True

# now that prices are compared to targets out of the log format in a comprehensible format, let's compare
# can compare manually with output tables, or add a new column with residual values

#df_pf['Residuals'] = y_hat_test - y_test # predictions - targets
#print('\n',df_pf.head())

# improved clarity:
df_pf['Residual']=df_pf['Target'] - df_pf['Prediction']
print('\n',df_pf.head())


# these residuals are the heart of the algorythm, and udnerstanding & evaluating them well is the key to ML
# we'll show additional info about them by calculating their percentages
df_pf['Difference in %'] = np.absolute( df_pf['Residual'] / df_pf['Target'] * 100 )
print('\n',df_pf.head())

# analyze the final table's description:
print('\n',df_pf.describe())

# sort the table by difference percentage 
#df_pf = df_pf.sort_values(by=['Difference in %'])
#print('\n','Sorted by Difference Percentage:','\n',df_pf)
# to see all the rows possible {{ pandas cuts off middle by default }} include the following option before printing the DataFrame
# also can set float value to 2 decimals, like so:
pd.options.display.max_rows = 999 # row count def
pd.set_option('display.float_format', lambda x: '%.2f' % x) # float def

df_pf = df_pf.sort_values(by=['Difference in %'])
print('\n','Sorted by Difference Percentage:','\n',df_pf)