Adjusted variables to remove empty values, and leveled out exponential distributions with upper & lower limits on the features
```python
import numpy as np
import pandas as pd
import statsmodels.api as sm
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.linear_model import LinearRegression
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