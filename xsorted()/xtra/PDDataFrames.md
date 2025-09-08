```python
import numpy as np
import pandas as pd

# Pandas series are similar to DataFrames but limited by one column
# DataFrames are a collection of series or columns
# it can contain variables & information on the variables within it
# values of series can be refernced by a single indice
# DatFrames require the indices of the row AND the column
# very close to a matrix, but not a matrix

array_a = np.array([[1,2,3],[4,5,6]])
print('numpy array;')
print(array_a)
print(type(array_a))

array_d = pd.DataFrame(array_a) # make it a DataFrame
print('\nPanda DataFrame from nd array:')
print(array_d)
print(type(array_d))

df = pd.DataFrame(array_a,columns=['Column 1','Column 2','Column 3'],index=['row1','row2'])
print('\nRenamed Columns of df:\n',df)

r_data = pd.read_csv('/Volumes/HomeXx/compuir/xsell/Lending-company.csv', index_col='LoanID') # read and import data with indices set to Loan ID

data = r_data.copy()

print(data.head()) # first few rows
print(data.index) # returns the indexing for the df
print(data.columns) # returns all column titles
print(data.dtypes) # returns all row labels
print(data.values) # makes all rows into arrays, and stores these arrays in another 2D array, similar as to_numpy()
print(data.shape) # returns dimensions: (1043, 14) 1043 rows, 14 columns