```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
sns.set()
from sklearn.cluster import KMeans

raw_data = pd.read_csv('/Volumes/HomeXx/compuir/3.01. Country clusters.csv')

# we have country name, Latitude, Longitude, and Language Features

data = raw_data.copy()

data_mapped = data.copy()

data_mapped['Language'] = data_mapped['Language'].map({'English':0,'French':1,'German':2})

x = data_mapped.iloc[:,3:4] # slice all rows, and last column
# could change to [:,1:4] and cluster off 3 features, or last 3 rows

kmeans = KMeans(3)
kmeans.fit(x)

identified_clusters = kmeans.fit_predict(x)
print(identified_clusters)

data_with_clusters = data_mapped.copy()
data_with_clusters['Cluster'] = identified_clusters

print(data_with_clusters)

# plot on scatter of long and lat , but cluster based off langauge feature
# still shown on long x lat graph but colored by cluster
plt.scatter(data['Longitude'],data['Latitude'],c=data_with_clusters['Cluster'], cmap='rainbow') # plain color suckz
plt.xlim(-180,180)
plt.ylim(-90,90)
plt.show()
plt.close() # we see three clusters 