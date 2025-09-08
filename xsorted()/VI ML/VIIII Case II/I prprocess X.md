we want to predict the absenteeism, or probability someone will be absent on a given day

```python
import pandas as pd

raw_data = pd.read_csv('Volumes/HomeXx/compuir/Absenteeism_data.csv')

data = raw_data.copy()

pd.options.display.max_columns = None # max columns
#pd.options.display.max_rows = None # max rows
pd.options.display.max_rows = 15 # max rows

#data.drop(['ID'],axis=1) # drop the id column, temprorary
data = data.drop(['ID'],axis=1) # drop the id column, temprorary

#data_noage = data.drop(['Age'],axis=1) # drop the id column, temprorary
#data = data.drop(['Education'],axis=1) # drop the id column, temprorary
#print(data_noage.info()) # no missing values
#print(data.head()) # no missing values
#get just reason for absenteeism
res_col = data['Reason for Absence']


# check for missing values
#reason['check'] = reason.sum(axis=1)
#print(reason)
#sum = reason['check'].sum(axis=0)
#print(sum) # we saw 700, so we know that column *averages* one, but are they all one?
#unsum = reason['check'].unique()
#print(unsum) # returns ' [1] ' unique value, so every value is a 1 !
	#age = pd.get_dummies(data['Age'], drop_first=True).astype(int)
#print(age)
#age['check'] = age.sum(axis=1)
#print(age)
#print(age['check'].unique()) # one unique value
#print(age['check'].sum(axis=0)) # sum is 700 ; no missing values
# count unique values
#print(len(res.unique()))


# sort
#print(sorted(res))

# reason for absence is categorical values with numerical values
# well use dummy variables to sus out if any of these could be the root of the issue or correlate 
# the method we'll use is pandas get dummies 
# we can check teh values of this feature with summation of 1's and 0's to find missing or duplicate values
#print(data.columns.values)
#drop dummy var to prevent multi-collinearity
reason_col = pd.get_dummies(data['Reason for Absence'], drop_first=True).astype(int)
#print(reason_col.columns.values)

data = data.drop(['Reason for Absence'],axis=1)

# groups 1-14 are related to diseases, groups 15-17 are related tp preganancy, group 18-21 are about poisoning, group 22-28 is appointments, consultations, etc.,
# we'll apply this classification to the Reason for Absence columns
reason_t_1 = reason_col.loc[:,:14].max(axis=1) # all columns between columns 1 and 14
reason_t_2 = reason_col.loc[:,15:17].max(axis=1) # all columns between columns 15 and 17
reason_t_3 = reason_col.loc[:,18:21].max(axis=1) # .max() returns series's, not dataframes
reason_t_4 = reason_col.loc[:,22:].max(axis=1) # instead of having all columns be considered, we determine if any of the columns in this class were present during the analysis
#print(reason_t_1, reason_t_2, reason_t_3, reason_t_4)

data['diseases'] = reason_t_1
data['pregnancy'] = reason_t_2
data['poisoning'] = reason_t_3
data['additional'] = reason_t_4
#or
#ndata = pd.concat([data, reason_t_1, reason_t_2, reason_t_3, reason_t_4], axis=1)

# add them to the data 
print(data.columns.values)
#print('\n\n')
#print(ndata.columns.values)
#print(ndata.head())

age = pd.get_dummies(data['Age'], drop_first=True).astype(int)

#Index([28, 29, 30, 31, 32, 33, 34, 36, 37, 38, 39, 40, 41, 43, 46, 47, 48, 49, 50, 58]
young = age.loc[:,28:32].max(axis=1)
middle = age.loc[:,33:47].max(axis=1)
old = age.loc[:,48:58].max(axis=1)

data['young'] = young
data['middle'] = middle
data['old'] = old


#reorder the dataframe's column titles
#['Date' 'Transportation Expense' 'Distance to Work' 'Age' 'Daily Work Load Average' 'Body Mass Index' 'Education' 'Children' 'Pets' 'Absenteeism Time in Hours' 'diseases' 'pregnancy' 'poisoning' 'additional' 'young' 'middle' 'old']
d_ordered = ['diseases', 'pregnancy', 'poisoning', 'additional', 'Date', 'Transportation Expense', 'Distance to Work', 'Age', 'Daily Work Load Average', 'Body Mass Index', 'Education', 'Children', 'Pets', 'young', 'middle', 'old', 'Absenteeism Time in Hours']

data = data[d_ordered]
#print(data.columns.values)


checkpoint = data.copy()

#Date
#print(type(checkpoint['Date'])) # <class 'pandas.core.series.Series'>
# what about type of each of the values?
#print(type(checkpoint['Date'][0])) # <class 'str'>
#print(checkpoint['Date'][0])
#print(checkpoint['Date'][30])
# lets convert these strings into timestamps using pd.to_datetime()
checkpoint['Date'] = pd.to_datetime(checkpoint['Date'], format='%d/%m/%Y')

# extract a month value
#print(checkpoint['Date'][0].month) # 1-12, not 0-11 btw
# add a month value column
list_months = []
for i in range(700):
	list_months.append(checkpoint['Date'][i].month)
#print(list_months)

# add it to the dataframe
checkpoint['Months'] = list_months
#print(checkpoint.head())

# do the same for weekdays
# make a function to return the day of the week from a given date
def weekday(date_value):
	return date_value.weekday()

# make a new Day of the Week column equal to the function weekday applied to every date
checkpoint['Day of the Week'] = checkpoint['Date'].apply(weekday)

checkpoint = checkpoint.drop(['Date'],axis=1)

print(checkpoint.columns.values)

headers = ['diseases', 'pregnancy', 'poisoning', 'additional', 'Months', 'Day of the Week', 'Transportation Expense', 'Distance to Work', 'Age', 'Daily Work Load Average', 'Body Mass Index', 'Education', 'Children', 'Pets', 'young', 'middle', 'old', 'Absenteeism Time in Hours']

checkpoint = checkpoint[headers]

print(checkpoint.columns.values)

df_reason_date_mod = checkpoint.copy()


# education
df_reason_date_mod['Education'].unique()# 4 values
df_reason_date_mod['Education'].value_counts()# most are highschool, so ' standardize '

df_reason_date_mod['Education'] = df_reason_date_mod['Education'].map({1:0, 2:1, 3:1, 4:1})

data_proc = df_reason_date_mod.copy()

# export and save as csv file
data_proc.to_csv('/Volumes/HomeXx/compuir/xsell/data_proc.csv')

```