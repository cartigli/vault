[overfit] : the data focuses on the problem so specifically it misses the idea; cannot generalize; accuracy seems too good
		found with training data, or testing inputs
		i.e., can nail the training data very well; cannot accurately output anything for testing data
[underfit] : the model did not capture the underlying logic of the problem; very low accuracy
		found by it cannot accurately answer
		low accuracy on training and test data

One way to eliminate these, or identify, is to test out training data
		this suggests splitting the data set into two components; data to run the 'regression' or 'ML' against, and another set of similar data to see how it handles the problems
```python
import numpy as np
from sklearn.model_selection import train_test_split

# generate data to split
a = np.arange(1,101) # .arange() is similar to the range() fx but defaults to nd array for formatting
print('np array a:','\n',a,'\n')
b = np.arange(501,601)
print('np array b:','\n',b,'\n')

# split the data
# train_test_split splits arrays or matrices into random train & test subsets
#test_a = train_test_split(a)
#print('train/test data split a:','\n',test_a,'\n')
#test_b = train_test_split(b)
#print('train/test data split b:','\n',test_b,'\n')

# better practice:
# by default, the train_test_split() fx's first array is the training data and teh second array is the testing data
a_train, a_test = train_test_split(a)
print('training splits for a:','\n')
print('training data a-split:',a_train)
print('testing data a-split:',a_test)

b_train, b_test = train_test_split(b)
print('\n','training splits for b:','\n')
print('training data b-split:',b_train)
print('testing data b-split:',b_test)
print('\n')

# explore the results:
print('Default train_test_split() shape:')
print('a-train shape:',a_train.shape)
print('a-test shape:',a_test.shape)
print('\n')

print('b-train shape:',b_train.shape)
print('b-test shape:',b_test.shape)
print('\n')

# if 75 / 25 was not the desired split, train_test_split accepts arguments for the distribution among the two:
c = np.arange(111,222) # new numpy array
c_train, c_test = train_test_split(c, test_size=0.1)

# explore this new split:
print('Split with 90% training and 10% testing data:')
print('c-train shape:',c_train.shape)
print('c-test shape:',c_test.shape,'\n')

# if we needed our arrays to be in a certain order, like for a time series, then we would NOT want the default shuffling behavior of train_test_split()
# removing the shuffling function sets it back to ' True ' because that is the default
# in normal cases, shuffling helps with training as it can't learn patterns from the order of the data if irrelevant
d = np.arange(222,333) # new numpy array
d_train, d_test = train_test_split(d, test_size=.4, shuffle=False)

print('Arrays without shuffling enabled:')
print('d-train without shuffling:','\n',d_train)
print('d-test without shuffling:','\n',d_test,'\n')

# if we needed to have the data shuffled in THE SAME WAY everytime, then add the random_state argument to the train_test_split fx
e = np.arange(333,444)
e_train, e_test = train_test_split(e, test_size=.4, shuffle=False, random_state=42)

print('Shuffled array on random_state = 42 ( will shuffle the same way every time) ;):')
print('e train array:','\n',e_train)
print('e test array:','\n',e_test)


# simplification ; efficiency :
# the functions below can be combined into one:
#a_train, a_test = train_test_split(a) ;
#b_train, b_test = train_test_split(b)
# together, they could be one line and command:
a_train, a_test, b_train, b_test = train_test_split(a, b, test_size=.3, random_state=42)

# check out results:
print('\n','Combined line for generating test and train data results:')
print(a_train.shape, a_test.shape, b_train.shape, b_test.shape)
# this is also helpful because a is locked in with b ; a[25] = b[25] , a[1] = b[1] ; meaning outputs can be coordinated with inputs, correct answers can be easily connected, and simplifies intuition of processi