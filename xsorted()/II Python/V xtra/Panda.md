```python
import numpy as np
import pandas as pd

products = ['A','B','C','D']
print('pd series')
print(type(products)) # list
print(products) # horizontal

# what if we want a series
product_categories = pd.Series(products)
print('\npd series products')
print(type(product_categories)) # series, object [non-numeric data]
print(product_categories) # vertical, and indices added

d_rates = pd.Series([40,70,30,50])
print('\npd series numerical')
print(type(d_rates)) # series of numbers
print(d_rates) # still vertical, still given indices


array_a = np.array([10,20,30,40])
print('\nnd array')
print(type(array_a))
print(array_a)

series_a = pd.Series(array_a) # adding brackets [array_a] would make the output horizontal
print('\npd series of nd array') # only change is output is an object not int64
print(type(series_a)) # but both are still pd.series
print(series_a)

# series have a set-in-stone order that is defined with the indices

# attributes are passive, metadata
# methods are active, have functionalities and behaviors
# methods and functions 
# functions
# functions are independent, not associated with object of any class
# methods
# can manipulate the abject's state and access its data

start_date_deposits = pd.Series({
	'7/4/2014' : 2000,
	'8/4/2014' : 3000,
	'9/1/2014' : 3000,
	'9/7/2014' : 4000,
	'10/7/2014' : 2000,
	'10/14/2014' : 1500,
	'10/29/2014' : 3000,
	'11/20/2014' : 2000
	})
print(start_date_deposits)
print('\nSum:\n',start_date_deposits.sum()) # pandas methods
print('\nMin:\n',start_date_deposits.min())
print('\nMax:\n',start_date_deposits.max())
print('\nIndice of Min:\n',start_date_deposits.idxmin()) # holy shit
print('\nIndice of Max:\n',start_date_deposits.idxmax()) # dates are the indices?

# Pandas steps on NumPy, so some of its methods are duplicate between the two
# like min, max, sum
# it also has non-mathematic methods
print('\nHead:\n',start_date_deposits.head()) # first few
print('\nHead 7:\n',start_date_deposits.head(7)) # first few
print('\nTail:\n',start_date_deposits.tail()) # last few
print('\nTail n = 2:\n',start_date_deposits.tail(n=2)) # last few

# Pandas series are similar to DataFrames but limited by one column
# DataFrames are a collection of series or columns
# it can contain variables & information on the variables within it
# values of series can be refernced by a single indice
# DatFrames require the indices of the row AND the column