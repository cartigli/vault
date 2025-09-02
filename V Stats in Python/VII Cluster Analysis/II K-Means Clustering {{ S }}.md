most popular method for clustering

steps:
	choose the number of clusters
	specify the cluster seeds [ initial centroid seed ]
	assign each point to one of the available centroids
	adjust centroids given their selected connected points
		repeat the last two steps
		
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



# long and lat are like coordinates on Earth's plane
# we can pretend they are x and y for a scatter plot if we set the scatter plot's domain to be the same as Earth's
plt.scatter(data['Longitude'],data['Latitude'])
plt.xlim(-180,180)
plt.ylim(-90,90)
plt.show()
plt.close() # we see three clusters 



# select features for clustering ; we just saw long - lat was a good clustering , so let's use them as x and y
# pandas' DataFrame.iloc(row indices, column indices) slices the data frame, given rows and columns to be kept
# column indicies are country [0], lat [1], long [2], lang [3]
x = data.iloc[:,1:3] # first arg is ' : ' because we want all rows, second arg is columns with indices of 1 & 2 ; 1:3 because indices of 1 -> last indice + 1
# x = the columns lat and long with all rows

print(x)



# clustering 
kmeans = KMeans(3) # Kmeans from sklearn , 2 is cluster count , k
# can be changed and rerun easily

# now apply the data we cleaned {{ x }} to fit the KMeans fx which was applied to an object ; kmeans
kmeans.fit(x) # this outputs ' KMeans(n_clusters=2) ' , meaning the clustering completed



# clustering results
identified_clusters = kmeans.fit_predict(x)
print(identified_clusters) # output [0 0 0 0 0 1]
# this is read as the first five variables were placed in cluster 0 , while the last variable was placed in cluster 1

data_with_clusters = data.copy()
data_with_clusters['Cluster'] = identified_clusters

print(data_with_clusters)
#     Country  Latitude  Longitude Language  Cluster
#0        USA     44.97    -103.77  English        0
#1     Canada     62.40     -96.80  English        0
#2     France     46.75       2.40   French        0
#3         UK     54.01      -2.53  English        0
#4    Germany     51.15      10.40   German        0
#5  Australia    -25.45     133.11  English        1

# we can see that all countries but Australia were clustered in cluster 0, while cluster 1 was given Australia alone
# now do the same graph as before , but with an additional variable specifying color to be chosen by a varibale , specifically the cluster variable

plt.scatter(data['Longitude'],data['Latitude'],c=data_with_clusters['Cluster'])
plt.xlim(-180,180)
plt.ylim(-90,90)
plt.show()
plt.close() # we see three clusters 


plt.scatter(data['Longitude'],data['Latitude'],c=data_with_clusters['Cluster'], cmap='rainbow') # plain color suckz
plt.xlim(-180,180)
plt.ylim(-90,90)
plt.show()
plt.close() # we see three clusters 