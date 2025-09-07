```python
import os
import pandas as pd
from sklearn import preprocessing

# load the dataset
data = pd.read_csv('/Volumes/HomeXx/compuir/Audiobooks_data.csv', delimiter=',')

print(data.columns)
print(data.shape)