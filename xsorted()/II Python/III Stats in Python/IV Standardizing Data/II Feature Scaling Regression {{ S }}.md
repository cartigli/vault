standardize the data from {{ III Regression with Sklearn }}
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
sns.set()
from sklearn.linear_model import LinearRegression

data = pd.read_csv('/Volumes/HomeXx/compuir/Downloads/1.02. Multiple linear regression.csv')

# declare variables
x=data[['SAT','Rand 1,2,3']]
y=data['GPA']

# import the sklearn standardization module
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler() # create empty StandardScalar object
# ' scalar ' can now be used to scale our data
# this will subtract the mean and divide by sigma for every variable its applied to

# employ the scaling mechanism
scaler.fit(x) # calculates the mean and std dev for each feature

# apply the mechanism ; no longer an empty object
# to apply, use the StandardScalar.transform() fx ; which performs a feature - wise scaling
x_scaled = scaler.transform(x)
# print(x_scaled) <= prints all 84
# print(x_scaled.head()) <= Pandas method, not for np arrays
print(x_scaled[:5]) # slice first five elements ; 0 - 5