[ Flat and Hierarchal ]
	KMeans is flat as in we choose the cluster, and there is no hierarchy

[Hierarchal]
	devlopped first 
	common ex. is the taxonomy of the animal kingdom
	**animals** 
		**mammals** , birds , fish
			**cats** , dogs , whales
				tigers , leopards , lions
	two types of hierarchal clustering:
		[Agglomerative]
			' bottom up'
				start from different dog and cat breeds, up and up, until only the animals cluster is left 
				Divisive and Agglomerate clustering should approximate to the same final answers, but Agglomerate, or bottom up clustering, is much easier to compute mathematically 
		[Divisive]
			' top down '
				start with category, i.e., Dinosaurs, and split into 2 groups, which is split again, etc., etc., until every observation is in its own cluster
				not the fastest, KMeans Elbow technique does this in real time to find optimal num of clusters

[Agglomerate] Clustering
	starting with every observation, n, in its own category, we start by grouping observations by their similarities, which can mean many things but mathematically is the [Euclidean Distance]. 
		We cluster the closest pair of observations, n, resulting in a total of n - 1 clusters
			we repeat until all observations are in the same cluster
				this forms a [Dendrogram]
					the Dendrogram holds All Solutions
Bigger the difference between two lengths, the bigger the dif between their features

					Dendrogram
					       |                    row0
			|-----------------------|   row1
		|---------------|         |   row2
	|-----|           |         |   row3
	|   |----|      |----|      |   row4
	UK Fran Germ   US   Can    Aust
-
	if we cut out dendrogram on row 0, there is 1 cluster 
	if we cut out dendrogram on row 1, there are 2 clusters 
	if we cut out dendrogram on row 2, there are 3 clusters 
	if we cut out dendrogram on row 3, there are 4 clusters 
		and if we cut out dendrogram on row 3, there are 4 clusters 
-
	the two most related groups are US and Canada, and France and Germany
	Australia is the furthest related from any other observations

Pros
hierarchal clustering shows all the possible links between clusters
we understand the data we're working with better, like how it is inter-related
no need to preset the number of clusters, like kmeans 

Cons
	scalability is a huge weakness, i.e., with 1000+ observations