pros
	fast dimple, widely available, easy to implement, always yields a result
cons:
	we need to pick k 
		remedy: elbow helps, but not scientific
	Sensitive to initialization == randomly choosing centroid seeds can mess with the analysis
		remedy: k-means++ - determines optimal centroid means mathematically
	sensitive to outliers
		if one value is too far, it will just be given its own cluster usually 

To Standardize or Not to Standardize
	imagine a plot of house size vs house price:
		House A: 500 sq ft, $50,000
		House B: 500 sq ft, $100,000
		House C: 1200 sq ft, $50,000
		House D: 1200 sq ft, $100,000
			if we tried to cluster with 2 clusters, it would be difficult because all points are equidistant, and so could be clustered in almost any combination with equal WCSS
				probably just cluster AB and CD
			if we standardized the x axis, size, we would get the following:
					House A: -1 sq ft, $50,000
					House B: -1 sq ft, $100,000
					House C: 1 sq ft, $50,000
					House D: 1 sq ft, $100,000
						in this configuration, A & C are much closer than A & B or C & D, so
						the new clustering would be AC and BD
				if we standardize the y axis as well, we get the following:
						House A: 500 sq ft, -1
						House B: 500 sq ft, 1
						House C: 1200 sq ft, -1
						House D: 1200 sq ft, 1
							now, this is a perfect square, and AB = AC, and DB = DC
							also, CA = CD, and BA = BD
				scale affects the values in the same way and distorts the ideal clustering configuration
					the range of the values becomes the weights, if size and price were both on a 100,000 scale, then price's would tell far more than land size, as land size is so small compared to the scale of 100,000, while the price is more appropriately distributed 0 - 100,000
	In summary, if we know a variable is more important to another, do not standardize
		in price vs size, the land size could be considered crucial, and so shouldn't have been standardized as it informs price
	Otherwise, standardization is a reliable and useful method for unknown importance in kmeans clustering
