[ content ] = topic, main point, key component

new field kinda
- 25 years ago, someone called a 'statistician' would be responsible for cleaning and gathering data sets
	- statistician -> data mining specialist 
	- data mining -> predictive analytics
	- predictive analytics -> data scientist 
		- hr managers can mislabel positions due to confusion/lack of clarity between roles
- major fields/common confusion
	- business analytics
	- data analytics
	- data scientist
	- business intelligence
	- machine learning

Business Intelligence & Data Analysis
SQL, Python, Panda, NumPy, 

common keywords: data, algorithm, insight

30 observations - each gave insight of loyalty & satisfaction
```
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
sns.set()
from sklearn.cluster import KMeans
from sklearn import processing


data = pd.read_csv('Example.csv') 

plt.scatter(data['Satisfaction'],data['Loyalty'])
plt.xlabel(;Satisfaction')
plt.ylabel('Loyalty')

# **scatter plot output here**

x = preprocessing.scale(data)

# using the kmeans cluster, could do same with colors for highxhigh, lowxhigh, highxlow, andlowxlow
# lowxlow = alienated, disloyal & disatisfied 
# highxlow = satisfied, but disloyal
# lowxhigh = disatisfied, but loyal
# highxhigh = fans
	# highxlow could be fans if loyalty improved
	# lowxhigh could be fans if satisfaction approved
```