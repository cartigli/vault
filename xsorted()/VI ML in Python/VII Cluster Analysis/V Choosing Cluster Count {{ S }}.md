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

x = data.iloc[:,1:3]

# create an empty list for WCSS
wcss = []

# the loop logic
for i in range(1,7):
	kmeans = KMeans(i) # calculate clustering for i in 1 - 7
	kmeans.fit(x) # fit the model
	wcss_iter = kmeans.inertia_ # calculate the wcss for i in 1 - 7
	wcss.append(wcss_iter)

print(wcss) # output array below:
#[42601.91356666667, 17243.964500000002, 288.1052333333333, 111.91233333333332, 38.50624999999999, 0.0]
# cluster 1 starts the highest, rapidly decreases from 1 to 2 and 2 to 3, but slows down for 3 to 4 and 4 to 5. 5 to 6 is 0, as 6 clusters for 6 variables is perfect WCSS without any gained information


# graph it:
number_clusters = range(1,7)
plt.plot(number_clusters, wcss) # plot 1 - 7 against array above ; WCSS
plt.title('Elbow Method',fontsize=15)
plt.xlabel('Num of Clusters',fontsize=10)
plt.ylabel('WCSS',fontsize=10)
plt.show()
plt.close()

# from the graph, we know we should choose either k = 2 or k = 3 clusters
# k = 1 or k = 4 or k = 5 would be incorrect and suboptimal cluster counts