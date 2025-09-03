Final Goal : Maximize the similarities of observations within the clusters and simultaneously maximize the dissimilarity between clusters

well check out...
	clustering problems
	how to perform cluster analysis
	how to find optimal number of clusters
	how to identify appropriate clusters
	how to interpret results

the libraries we'll use are pandas and sci-kit learn

an example of useful clustering 
we have 6 observations; US, Canada, UK, Germany, France, Australia

could cluster by continent, by language, by currency, etc.,

what if limited by two clusters?
could be US, Canada, Germany, France, UK, - cluster 1
Australia - cluster 2
cluster 1 = northern hemisphere , cluster 2 = southern

Why's it useful?
	two applications:
		market segmentation
			marketing is shit, but you realize there are two major clusters of customers to focus on, marketing changes their strategies, company can focus on high paying customers who are likely to purchase more
		image segmentation
			idk how to show this concept in md ; above ex is better anyway

Clustering does not use labels ; akin to unsupervised ML compared to Categorization 


Methods:
imagine we have two points on a graph: (3, 4.5) and (10, 2.5)
how do we measure the difference between these two points?
	build a right triangle, lengths of 10 - 3 and 4.5 - 2.5 , or 7 and 2
		[Pythagorean Theorem] $\sqrt{7^2 + 2^2} = \sqrt{49 + 4} = \sqrt{53} = 7.28$
		The [Euclidian Distance] = 7.28, or the distance between the two points
		generalized, if the points were ($x_2, y_2$) and ($x_1, y_1$), the Euclidean Distance would be equal to $\sqrt{ ( x_2 - x_1 )^2 + (y_2 - y_1)^2 }$

in 2d space; d(A,B) = d(B,A) = $\sqrt{ ( x_2 - x_1 )^2 + (y_2 - y_1)^2 }$
in 3d space; d(A,B) = d(B,A) = $\sqrt{ ( x_2 - x_1 )^2 + (y_2 - y_1)^2 + (z_2 - z_1 )^2 }$
in N-Dimensional space, the formula's pattern would continue and calculate the square root of the squared difference of each dimension N

in nd space; d(A,B) = d(B,A) = $\sqrt{ ( a_2 - b_1 )^2 + (a_2 - b_1)^2 + . . . (a_n - b_n )^2 }$
with clustering, we'll find the distance between clusters of n dimensional space where n = the number of features in the data set

[Centroid]
	in our example, the centroid is the point on the line between our two points which is halfway between both of them
	our line was 7.28, so the centroid of our two points is $\frac{7.28}{2} = 3.64$
	going from either point, if the line connecting them were 3.64 units long, it would point to exactly their centroid
	the heart of whatever cluster your analyzing = the Centroid