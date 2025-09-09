```python
import pandas as pd

# data selection is selecting rows, items, values, or columns of a dataset
# specify by row or column indice
r_data = pd.read_csv('/Volumes/HomeXx/compuir/xsell/Lending-company.csv', index_col='StringID')

data = r_data.copy()

#print(data.Product)
#print(data.Location)
# or
#print(data['Product'])
#print(data['Location'])
#print(data['location']) # returns error
#print(data[['Location','Product']])
#print(data['Location','Product']) # error
loc_prod = data[['Location','Product']]
#print(loc_prod)

# .iloc[]
# .iloc[] is an attribute indexer ; i for index, loc for location
# if we want the first column:
#print(data.iloc[1]) # just second column | returns column
#print(data.iloc[1,3]) # second column, fourth row | returns value


#print(data.iloc[1,:]) # data from all columns
#print(data.iloc[:,3]) # data from second column

# .loc[] is similar but only by index
print(data.loc['LoanID_3',:])
print(data.loc['LoanID_3','Region']) # returns load3's region: Region 3