who knows what we did here tbh
```python
import numpy as np
import pandas as pd
import statsmodels.api as sm
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.cluster import KMeans
from sklearn import preprocessing

raw_data = pd.read_csv('/Volumes/HomeXx/compuir/iris-dataset.csv')

print(data) # sepal length, sepal width, petal length, petal width

data = raw_data.copy()

data_s = data[['sepal_length','sepal_width']]

data_p = data[['petal_width','petal_length']] # ended up not using

plt.scatter(data['petal_width'],data['petal_length'])
plt.title('Petal')
plt.show()
plt.close()

plt.scatter(data['sepal_width'],data['sepal_length'])
plt.title('Sepal')
plt.show()
plt.close()

x = data_p.copy()
x1 = data_s.copy()

kmeans = KMeans(2)

kmeans.fit(x)

petal_c = kmeans.fit_predict(x)

kmeans.fit(x1)

sepal_c = kmeans.fit_predict(x1)

data['Sepal_c'] = sepal_c
data['Petal_c'] = petal_c


plt.scatter(data['petal_width'],data['petal_length'], c=data['Petal_c'], cmap='rainbow')
plt.title('Petal')
plt.show()
plt.close()

plt.scatter(data['sepal_width'],data['sepal_length'], c=data['Sepal_c'], cmap='rainbow')
plt.title('Sepal')
plt.show()
plt.close()