removed extraneous prints for columns and values, as well as checks for new shapes / altered features
added linear regression
added import for scaling {{ scaler }} ; added import for train_test splitting ; made and analyzed results of the summary table

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
print('before dummies:','\n',data_no_multicollinearity.head(),'\n')
print('before dummies:','\n',data_no_multicollinearity.columns.values,'\n')



# **adding dummies**

data_with_dummies = pd.get_dummies(data_no_multicollinearity, drop_first=True) # drop first for n - 1 dummies

# do a * very, very * manual adjustment to move the dependent var to the first pos
cols = ['log_price', 'Mileage', 'EngineV', 'Brand_BMW', 'Brand_Mercedes-Benz', 'Brand_Mitsubishi', 'Brand_Renault', 'Brand_Toyota', 'Brand_Volkswagen', 'Body_hatch', 'Body_other', 'Body_sedan', 'Body_vagon', 'Body_van', 'Engine Type_Gas', 'Engine Type_Other', 'Engine Type_Petrol', 'Registration_yes']

# set the preprocessed data to be the dummy var data with the rearranged columns
data_preprocessed = data_with_dummies[cols]


# **the meatty stuff**

# **The Linear Regressoin Itself**


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