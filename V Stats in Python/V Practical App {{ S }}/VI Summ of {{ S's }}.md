all together now {{ works with all graphs, print statements, DataFrames, and imported packages }}
```python
import numpy as np
import pandas as pd
import statsmodels.api as sm
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.linear_model import LinearRegression
from sklearn.preprocessing import StandardScaler
from sklearn.model_selection import train_test_split
from statsmodels.stats.outliers_influence import variance_inflation_factor
sns.set()

raw_data = pd.read_csv('/Volumes/HomeXx/compuir/1.04. Real-life example.csv')
print(raw_data.head()) # get first five rows / columns

print('\n','Columns labels:','\n',raw_data.columns) # info was cut short by output width
# we have Brand, Price, Body, Mileage, Engine V, Engine Type, Registration, Year, & Model
# we want to predict price
# Brand, Mileage, Engine V[olume], Year are all relevant
# rest are categorical ; deal with on case by case basis

#print(raw_data.describe()) # only outputs descriptions of numerical data
#print(raw_data.describe(include='all')) # option to describe all data
# this showed model has 312 unique values for 4k data points , not useful

# drop Model using Pandas
# using pandas' .drop() method
# specify the column, and then specify the axis
data = raw_data.drop(['Model'],axis=1)
print('\n',data.head())

# find empty values or missing data
data.isnull()
print('\n','Empty values or cells:','\n',data.isnull())

# shows table and true and false values ; true stands for missing and false stands for available
# true = 1 and false = 0, so the method below can count missing values
data.isnull().sum() # add all 'True's' together
print(data.isnull().sum()) # price and engine v only are missing values

# remove entries with missing values
# dropping observations { rows } , not columns, so axis = 0
# data_no_mv = data no missing values
# .dropna() drops values of NA along the axis = 0
data_no_mv = data.dropna(axis=0)
print(data_no_mv.describe(include='all'))

# make distribution plot for Price
print('\n','Data plot of Prices before adjustments:','\n')
sns.displot(data_no_mv['Price'])
print(sns.displot(data_no_mv['Price']))
plt.show() # show the created graph
# we see an exponential slope, so this will be difficult for regressional analysis {{ most certainly linear regression }}
# due to outliers and extreme values ; inflate and distort regression
# could remove the top 1% of variables
plt.close()

# pandas' DataFrame.quantile() method returns the value at the given quantile, i.e., np.percentile = 0.25 is 25% quantile
q = data_no_mv['Price'].quantile(0.99) # take bottom 99% from Prices
data_1 = data_no_mv[data_no_mv['Price']<q] # take the Prices of data_no_mv that are less than the quantile {{ defined above }} and bind to data_1

data_1.describe(include='all')
print(data_1.describe(include='all'))

# check new distribution of consolidated price values
print('\n','Data plot of Prices after adjustments:','\n')
sns.displot(data_1['Price'])
print(sns.displot(data_1['Price']))
plt.show()
plt.close()

# repeat process for Mileage
q = data_1['Mileage'].quantile(0.99)
data_2 = data_1[data_1['Mileage']<q] # take bottom 99% from Mileage
print(data_2.describe(include='all'))

print('The mileage plot before adjustments:','\n')
sns.displot(data_no_mv['Mileage'])
plt.show()
plt.close()

print('The mileage plot after adjustments:','\n')
sns.displot(data_2['Mileage'])
#print(sns.displot(data_2['Mileage']))
plt.show()
plt.close()

# engine volume holds a lot of values around 99.99 ; these are likely false or meant to be 0 or null entries
# try placing upper limit to extrapolate extraneous entries
# use data 2 to continue with creatoin of cleaned data
data_3 = data_2[data_2['EngineV']<6.5] # hardcoded rather than quantile

print('\n','Engine V plot before adjustments:','\n')
sns.displot(data_no_mv['EngineV'])
plt.show()
plt.close()

print('\n','Engine V plot after adjustments:','\n')
sns.displot(data_3['EngineV'])
plt.show()
plt.close()

# year
print('\n','Year plot before adjustments:','\n')
sns.displot(data_no_mv['Year'])
plt.show() # skewed left
plt.close()

# we'll do the same as Mileage but top 99%
q = data_3['Year'].quantile(0.01)
data_4 = data_3[data_3['Year']>q] # data_4 is Year's values above 1%

print('\n','Year plot after adjusments:','\n')
sns.displot(data_4['Year'])
plt.show()
plt.close()

# finally, set the new cleaned data to a new variable: cleaned_data
# drop=True forces the old index to be forgotten and replaced
data_cleaned = data_4.reset_index(drop=True)

# check the final cleaned data
print('\n','Cleaned data for analysis is ready:','\n')
print(data_cleaned.describe(include='all'))




# CHECK OLS ASSUMPTIONS


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


# DUMMY VARIABLES INTRO

data_no_multicollinearity = data_cleaned.drop(['Year'], axis=1) # drop the whole columns 
print('before dummies:','\n',data_no_multicollinearity.head(),'\n')
print('before dummies:','\n',data_no_multicollinearity.columns.values,'\n')

# adding dummies
# use pandas' .get_dummies(df[,drop_first]) method
# .get_dummies() spots all categorica variables & creates dummies for them
# if we have n categories for a feature, we create n - 1 dummies
# for brands, start with n and give all others 0
# continue for all brands
# for audi, we know if all dummies are 0, its an audi
# if we introduced another var, multicollinearity would occur between the dummy var and the additional audi var
data_with_dummies = pd.get_dummies(data_no_multicollinearity, drop_first=True) # drop first for n - 1 dummies
print('data with dummies:','\n',data_with_dummies.head())
# we see in the output that they have been replaced with dummies for every feature ; column count has multiplied
print(data_with_dummies.columns)

# do a * very, very * manual adjustment to move the dependent var to the first pos
cols = ['log_price', 'Mileage', 'EngineV', 'Brand_BMW', 'Brand_Mercedes-Benz', 'Brand_Mitsubishi', 'Brand_Renault', 'Brand_Toyota', 'Brand_Volkswagen', 'Body_hatch', 'Body_other', 'Body_sedan', 'Body_vagon', 'Body_van', 'Engine Type_Gas', 'Engine Type_Other', 'Engine Type_Petrol', 'Registration_yes']

# set the preprocessed data to be the dummy var data with the rearranged columns
data_preprocessed = data_with_dummies[cols]
print(data_preprocessed.head())


# THE MEATY SHIT

# LINEAR REGRESSION HERSELF


# define targets and variables:
targets = data_preprocessed['log_price'] # targets are the price { after log transformation }
inputs = data_preprocessed.drop(['log_price'],axis=1) # inputs = all but price


# scale the data
# set the scaler as an isntance of the StandardScaler class
scaler = StandardScaler()
scaler.fit(inputs) # calculates scaling rates, mean, sigma, etc.,
# don't scale price / targets

inputs_scaled = scaler.transform(inputs) # apply the scaling
# not usually advisable to standardize dummy inputs, for ml learning it doesn't matter as much
# once they are scaled, they loose their value as dummy variables


# complete a train & test split with train_test_split()
x_train, x_test, y_train, y_test = train_test_split(inputs_scaled, targets, test_size=0.2, random_state=365) # split train/test data 80/20 among inputs_scaled and targets so they are given to x_{train/test} and y_{train/test} respecitively


# create the regression
reg = LinearRegression() # initiate reg as an instance of LinearReg class
reg.fit(x_train, y_train) # create the regression on the split data
# note : this is a log regression due to the transformation we applied on price ; it is a Log-Linear Regression

y_hat = reg.predict(x_train) # check result by plotting predicted values against observations
# y_hat = the log-linear model's prediction of the input data : x_train

# show on scatter plot
# in the ideal case, this plot would be a concise and straight line going at exactly 45 degrees ; the model's predicitons {{ y_hat }} each meet with the {{ targets }} exactly on the opp. axis
# ours is not so, but kind of 
plt.scatter(y_train, y_hat)
plt.xlabel('Targets (y_train)',size=10)
plt.ylabel('Predictions (y_hat)',size=10)
plt.xlim(6,13)
plt.ylim(6,13)
plt.show()
plt.close()

# residual plot
# shows the points where the model innacurately predicted the output
# shows the difference between the targets and y_hat {{ predicitions }}
# or distribution of such risiduals
sns.displot(y_train - y_hat)
plt.title('Residual Probability Dist. Flow', size=10)
plt.show() # looks fairly normalluy distributed, but skewed left
plt.close()
# skewing left implies some values of y_hat were much larger than observed values, creating a negative skew ; it is overestimating the targets
# since no skew exists for the right, it does not underestimate often, or as often

# calculate the R^2
score = reg.score(x_train, y_train)
print('\n','R Squared:',score)
# output was 0.74499....
# therefore, our model explained 75% of the variability of data


# find the weights and bias
print('\n','Intercept:',reg.intercept_)
print('^ Scalar')

print('\n','Coeff:','\n',reg.coef_)
print('^ Array of all features and consequently, dummy vars','\n')


# create a summary table with features corresponding to weights
# create the pandas dataframe the input data's columns' values , or their titles. Name this 'Features'
reg_summary = pd.DataFrame(inputs.columns.values, columns=['Features'])
# see what this is before adding weights
print('Reg.Summary - no weights added:')
print('\n',reg_summary,'\n\n')

# add to the reg_summary table by introducing a new column; ' Weights '
reg_summary['Weights'] = reg.coef_ # set it equal the coefficients

print('Reg.Summary of dummy vars, vars, and their weights:','\n')
print(reg_summary)

#print('\nThe above is essentially uninterpretable ; the price has been transformed by a log fx and all inputs were standardized. A positive weight shows that as the feature increases in value, the log price, and therefore Price, increase. For example, as Engine V[olume] increases, the log price and Price increase accordingly. \n A negative weight shows that as the value of that feature\'s weight increases, the log price and in turn Price decrease.')

# dummy vars
# we dropped category per unique variable, when all dummy vars are 0 and the dropped var is 1 ; look at brand for example
print('\nBrand count:')
print(data_cleaned['Brand'].unique()) # shows us all unique brands in the brand category {{ after cleaning data }}
# from the reg_summary table, since we saw no audi variables, this means that Audi is the benchmark, since when making these variables we dropped 1, we know the dummy var is Audi when all other dummy vars for Brand are 0; Audi = 1
# this is interpreted as the following:
# positive dummy vars indicicates that the respective category of the  positive dummy var is more expensive than the benchmark Audi
# in our analysis and resulting values, only Mercedes and BMW are more expensive than Audi
# therefore, the negative values for dummy vars imply the respective categories of each dummy var are less expesive than Audi

print('\n',data_cleaned['Registration'].unique()) # returns yes & no
# since we only have two categories and dropped one, the only shown coefficient tells us all we need to know for registration
# the shown dummy var is yes, and with a positive value of 0.3, we can infer than cars with registration are more expensive than those without registration, since no registration {{ dropped var }} was the benchmark

# dummies should be compared to, and only to, other dummies of the same category, as that is how they were analyzed
# other vars can be compared together; Mileage has the most significant weight and therefore is our biggest indicator, or explanation, of Price
# this is followed by Registration, and then Engine V[olume]




# TESTING THE MODEL ; THE FINAL STAGE



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