```python
import numpy as np
import pandas as pd
import statsmodels.api as sm
import matplotlib.pyplot as plt
from sklearn.cluster import KMeans
import seaborn as sns
sns.set()

data = pd.read_csv('/Volumes/HomeXx/compuir/3.12. Example.csv')

print(data.head(10))
#   Satisfaction  Loyalty
#0             4    -1.33
#1             6    -0.28
#2             5    -0.99
#3             7    -0.29
#4             4     1.06
#5             1    -1.66
#6            10    -0.97
#7             8    -0.32
#8             8     1.02
#9             8     0.68
# we have 30 observations, and customer idicies with Satsifaction as a discrete variable and Loyalty as -2 to 2 [ standardized ]

plt.scatter(data['Satisfaction'], data['Loyalty'])
plt.title('Satisfaction vs Loyalty', fontsize=15)
plt.xlabel('Satisfaction', fontsize=10)
plt.ylabel('Loyalty', fontsize=10)
plt.show()
plt.close()


# select features
x = data.copy()


# clustering
kmeans = KMeans(2)


# perform the clustering
print('\n','kmeans.fit(x) results:','\n',kmeans.fit(x))


# get results
clusters = x.copy()
clusters['cluster_pred']=kmeans.fit_predict(x)

plt.scatter(data['Satisfaction'], data['Loyalty'], c=clusters['cluster_pred'], cmap='rainbow')
plt.title('Satisfaction vs Loyalty colored by Cluster', fontsize=15)
plt.xlabel('Satisfaction', fontsize=10)
plt.ylabel('Loyalty', fontsize=10)
plt.show()
plt.close()

print('^ This graph shows clustering as split down the satisfaction score of 6; scores on the right are red and on the left they are blue. This is likely because the satisfaction scores were not standardized, while loyalty scores were. This means the model likely only used on feature to cluster.')
print('Let\'s standardize the satisfaction:','\n')


from sklearn import preprocessing

x_scaled = preprocessing.scale(x) # .scale() standardizes with a mean of 0 and a standard dev of 1 by default for each variable [ column ] seperately

print('x_scaled results:','\n',x_scaled,'\n') # shows an array of standardized satisfaction scores while loyalty remain unchanged ; they were already standardized


# we still don't know the optimal cluster count, so let's find out:
wcss = []

for i in range(1,10): # 1 - 10 because 1 - 30 is excessive
	kmeans = KMeans(i) # calculate clustering for i in 1 - 7
	kmeans.fit(x) # fit the model
	#wcss_iter = kmeans.inertia_ # calculate the wcss for i in 1 - 7
	#wcss.append(wcss_iter)
	wcss.append(kmeans.inertia_)

print('wcss results:','\n',wcss)


# plot the results
plt.plot(range(1,10),wcss)
plt.title('Elbow Plot of Standardized Variabless')
plt.xlabel('Num of Clusters')
plt.ylabel('wcss')
plt.show()
plt.close() # shows points we could use at 2, 3, 4, and 5 Clusters


# explore clusterings of different cluster counts
kmeans_new = KMeans(2)
kmeans_new.fit(x_scaled)

clusters_new = x.copy() # build the dataset on og data, while clusters are calculated from standardized values
clusters_new['cluster_pred']=kmeans_new.fit_predict(x_scaled)

plt.scatter(clusters_new['Satisfaction'], clusters_new['Loyalty'], c=clusters_new['cluster_pred'], cmap='rainbow')
plt.title('Satisfaction vs Loyalty ; 2 clusters', fontsize=15)
plt.xlabel('Satisfaction', fontsize=10)
plt.ylabel('Loyalty', fontsize=10)
plt.show()
plt.close()


kmeans_new1 = KMeans(3)
kmeans_new1.fit(x_scaled)

clusters_new = x.copy() # build the dataset on og data, while clusters are calculated from standardized values
clusters_new['cluster_pred']=kmeans_new1.fit_predict(x_scaled)

plt.scatter(clusters_new['Satisfaction'], clusters_new['Loyalty'], c=clusters_new['cluster_pred'], cmap='rainbow')
plt.title('Satisfaction vs Loyalty ; 3 clusters', fontsize=15)
plt.xlabel('Satisfaction', fontsize=10)
plt.ylabel('Loyalty', fontsize=10)
plt.show()
plt.close()


kmeans_new2 = KMeans(4)
kmeans_new2.fit(x_scaled)

clusters_new = x.copy() # build the dataset on og data, while clusters are calculated from standardized values
clusters_new['cluster_pred']=kmeans_new2.fit_predict(x_scaled)

plt.scatter(clusters_new['Satisfaction'], clusters_new['Loyalty'], c=clusters_new['cluster_pred'], cmap='rainbow')
plt.title('Satisfaction vs Loyalty ; 4 clusters', fontsize=15)
plt.xlabel('Satisfaction', fontsize=10)
plt.ylabel('Loyalty', fontsize=10)
plt.show()
plt.close()


kmeans_new3 = KMeans(5)
kmeans_new3.fit(x_scaled)

clusters_new = x.copy() # build the dataset on og data, while clusters are calculated from standardized values
clusters_new['cluster_pred']=kmeans_new3.fit_predict(x_scaled)

plt.scatter(clusters_new['Satisfaction'], clusters_new['Loyalty'], c=clusters_new['cluster_pred'], cmap='rainbow')
plt.title('Satisfaction vs Loyalty ; 5 clusters', fontsize=15)
plt.xlabel('Satisfaction', fontsize=10)
plt.ylabel('Loyalty', fontsize=10)
plt.show()
plt.close()