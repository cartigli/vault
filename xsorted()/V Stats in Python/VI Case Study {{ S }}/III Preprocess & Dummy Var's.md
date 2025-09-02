comments cleaned ofc, plots removed and comparisons of log pricing introduction removed ; removed column check & all pre-cursing print statements
now, adding dummy variables ; adding print statements comparing the columns / column count before & after adding dummy vars ; moved log_price to the first pos of the columns for the future regression analysis {{ independent variable isolated a lil' }}

```python
import numpy as np
import pandas as pd
import statsmodels.api as sm
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.linear_model import LinearRegression
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


# Check OLS Assumptions

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