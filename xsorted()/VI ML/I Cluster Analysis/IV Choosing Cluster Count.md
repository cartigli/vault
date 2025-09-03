' elbow method '

minimizing distance between points in a cluster == maximizing distance between clusters

distance between points in a cluster is called
	' within-cluster sum of squares', or WCSS
		minimizing WCSS is the same as improving the clustering
			also, if 6 observations are given 6 clusters, WCSS will be 0 meaning perfectly clustered, but no information is gained through the analysis

If we plot WCSS against the number of clusters, we get a negative exponential graph
	As the number of clusters increases, WCSS drops to 0 and as the WCSS increases, the number of clusters decreases
		the ' elbow ' is the point in the slope of the graph where the WCSS can no longer improve with the given number of clusters
				```kmeans.inertia``` returns the WCSS for that cluster analysis, but ONLY that cluster analysis
					to calculate the graph, we need to actually calculate every k(1), k(2),... until we've exhausted our options, and compute the WCSS graph against that
					this can be accomplished through a for-loop
					exampled below

```python
# create an empty list for WCSS
wcss = []

# the loop logic
for i in range(1,7):
	kmeans = KMeans(i) # calculate clustering for i in 1 - 7
	kmeans.fit(x) # fit the model
	wcss_iter = kmeans.inertia_ # calculate the wcss for i in 1 - 7
	wcss.append(wcss_iter)
	