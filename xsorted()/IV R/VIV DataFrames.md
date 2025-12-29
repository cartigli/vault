```r
getwd()
setwd("/home/t")

# read the csv file into a data frame
data <- read.csv("Demographic-Data.csv", stringsAsFactors=TRUE)
# by default, stringsAsFactors is False so manually specifying as True 
# is needed for levels and factors to be shown 

# ---- Explorig the Data Frame ----
colnames(data) # column titles listed
rownames(data) # a row count essentially; useless

nrow(data) # counts the rows, returns an integer
# Imported 195 rows (traceback/error recovery)
ncol(data) # counts the columns

head(data) # first 6 rows with column titles
head(data, n=15) # non-default number of rows n
tail(data) # last 6 rows with column titles

str(data) # overview of each column & its data

summary(data) # summarizes contents;
# means, medians, modes, min, max for numerical 
# & categories + mode for categorical

# ---- Using the $ sign ----
x <- data[1,]
x # row one of the data; 1 for row num & no specification for column

y <- data[1:5,]
y # five rows of data

a <- data[,"Birth.rate"]
a # the entire Birth.rate column

b <- data[,3]
b # functionally equivalent to a

k <- data$Birth.rate
k # also equivalent

# select a single item of the column:
l <- data$Birth.rate[2]
l

# ^ equal to 
m <- data[2,"Birth.rate"]
m

# get the levels available for categorical columns
levels(data$Income.Group)


# ---- Basic Operations w.a DataFrame ----

# subset of first ten rows
data[1:10,]

# subset of rows 3 to 9
data[3:9,]

# subset of rows 4 and 99
data[c(4,99),]

# subset of first row
x <- data[1,] # drop=FALSE is not needed
is.data.frame(x) 
# [1] TRUE

y <- data[,1]
is.data.frame(y)
# [1] FALSE

# to ensure a column is a data frame, drop=FALSE must be specified
z <- data[,1,drop=FALSE]
is.data.frame(z)
# [1] TRUE


# ---- Operations ----

data$Birth.rate * data$Internet.users
data$Birth.rate / data$Internet.users
data$Birth.rate + data$Internet.users

# adding a column
data$New.Column <- data$Birth.rate + data$Internet.users

head(data)
# the New.Column shows up

# adding 5 values to a column of length 195
data$xyz <- 1:7 # throws an error becuase 195 is not divisible by 7

data$xyz <- 1:5
head(data, n=15)
# the values repeat until the column is filled

# removing a column
data$xyz <- NULL
data$New.Column <- NULL
head(data) # columns are gone



# ---- Filtering DataFrames ----
data$Internet.users < 2
# returns FALSE is greater and TRUE if less 
filter <- data$Internet.users < 2 # vector of T/F, length of the DataFrame

data[filter,] # returns values/rows where Internet.Users are less than 2
# for each row, if filter is TRUE, show the row, if FALSE, don't show

data[data$Internet.users < 2,] # equivalent

# all countries whose birthrate is over 40
data[data$Birth.rate > 40,]

# filter by both (two) parameters
data[data$Birth.rate > 40 & data$Internet.users < 2,]
# countries with Birth Rates over 40 and less than 2 Internet Users

data[data$Income.Group == "High income",] # only countries with High Income
data[data$Income.Group != "High income",] # only countries without High Income


# finding a specific country's data/row by name
data[data$Country.Name == "Malta",]
```

Visualizing with / Merging of Data Frames
```r
# ------ QPlot ------
library(ggplot2)
?qplot # deprecated according to the console

qplot(data=data, x=Internet.users)
qplot(data=data, x=Internet.users, y=Birth.rate)
# categorical on the x-axis, numerical data on the y-axis
qplot(data=data, x=Income.Group, y=Birth.rate)

# can change the size too, but should include I() to avoid extraneous legend
qplot(data=data, x=Income.Group, y=Birth.rate, size=I(2)) # treats I() as integer instead of a key

# can also change color, should use I() here as well
qplot(data=data, x=Income.Group, y=Birth.rate, size=I(2), color=I("red"))

# or can change the style/type of graph
qplot(data=data, x=Income.Group, y=Birth.rate, geom="boxplot", color=I("red"))

# ------ Visualizing What We Need ------

qplot(data=data, x=Internet.users, 
	  y=Birth.rate, 
      color=Income.Group, 
	  size=I(2)) # colors by groups of Income levels

# ------ Creating DataFrames ------

Countries_2012_Dataset <- # countries
Codes_2012_Dataset <- # codes
Regions_2012_Dataset <- # regions

newDF <- data.frame(Countries_2012_Dataset, 
                    Codes_2012_Dataset, 
                    Regions_2012_Dataset, 
					stringsAsFactors=TRUE)
head(newDF)
colnames(newDF)
colnames(newDF) <- c("country", "code", "region")
head(newDF) # manual renaming
# OR
rm(newDF)
newDF <- data.frame(country=Countries_2012_Dataset, 
                    code=Codes_2012_Dataset, 
                    region=Regions_2012_Dataset,
                    stringsAsFactors=TRUE)
head(newDF)
# same result, much cleaner and faster
# same naming convention works for r & c binds as well

summary(newDF) # needs stringAsFactors=TRUE to work correctly

# ------ Merging DataFrames ------

head(data)
head(newDF)

mergedf <- merge(data, newDF, by.x="Country.Code", by.y="code")
# merge <- merge(x-data, y-data, x.pair, y.pair) ; kinda similar to SQL
head(mergedf)
# duplicate country & region columns exist, and should be removed
# the merge was done by matching codes, so the dulpicate row is removed automatically
mergedf$country <- NULL
mergedf$region <- NULL

head(mergedf)

str(mergedf)

qplot(data=mergedf, 
		x=Internet.users, 
		y=Birth.rate, 
		color=region)

qplot(data=mergedf, 
		x=Internet.users, 
		y=Birth.rate, 
	    color=region,
        size=I(3),
        shape=I(19),
        alpha=I(0.6),
        main="Internet users vs. Birth Rates by Region")

qplot(data=mergedf, 
		x=Income.Group, 
		y=Birth.rate, 
		color=region,
        size=I(2))

qplot(data=mergedf, 
		x=Income.Group, 
		y=Birth.rate, 
		color=region,
		size=I(2),
		shape=I(19),
		alpha=I(0.7),
		main="Income vs. Birth Rate by Region")
```