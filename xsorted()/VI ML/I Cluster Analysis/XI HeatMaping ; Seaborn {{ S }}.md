```python
import numpy as np
import pandas as pd
import statsmodels.api as sm
import matplotlib.pyplot as plt
import seaborn as sns

# pd.read_csv(*.csv,index_col=..) loads a csv file as a dataframe; index_col is an argument which can specify a given column as an index of the data frame
data = pd.read_csv('/Volumes/HomeXx/compuir/Country clusters standardized.csv', index_col='Country')

x_scaled = data.copy()
x_scaled = x_scaled.drop(['Language'],axis=1)

# make a heat map of the data
# observations = countries, features = longitude and latitude
sns.clustermap(x_scaled)
#sns.clustermap(x_scaled, cmap='mako')
plt.show()
plt.close()
# dendrogram shown on the left, same exactly as we made on previous note
# at the top, another dendrogram connects both features as well
#         more on this later
# the colored blocks are the heatmap ; their key is in the upper left of the map