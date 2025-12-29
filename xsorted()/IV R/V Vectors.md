A sequence of data elements with the same basic type.

Sequenced and in a set order

Could be a vector of integers, doubles, characters ("Hello", "Five", "5" are all characters)

A single element, like 27 or "World" by themselves, is a single element vector.

```r

# c() 
MyFirstVector <- c(3, 45, 56, 293) 
# num [1:4] 3, 45, 56, 293

MyFirstVector
# [1] 3 45 56 293


is.numeric(MyFirstVector)
# [1] TRUE

is.integer(MyFirstVector)
# [1] FALSE

is.double(MyFirstVector)
# [1] True


MySecondVector <- c(3L, 45L, 56L, 293L)
# int [1:4] 3 45 56 293

is.integer(MySecondVector)
# [1] TRUE

is.double(MySecondVector)
# [1] FALSE

is.numeric(MySecondVector)
# [1] TRUE


v3 <- c("A", "B", "23")
# chr [1:3] "A" "B" "23"

is.character(v3)
# [1] TRUE

is.numeric(v3)
# [1] FALSE

v4 <- c("A", "B", "23", 6)
# chr [1:4] "A" "B" "23" "6" 
# automatically converted to the data type of previous elements


seq() # sequence - similar to ':'
rep() # replicate

seq(1, 15) 
# makes a sequence of numbers 1 - 15
# functionally equivalent to '1:15'


# seq() also has an option for 'stops'
seq(1, 15, 2)
# [1]  1  3  5  7  9 11 13 15

seq(1, 15, 7)
# [1] 1 8 15

seq(1, 15, 4)
# [1] 1 5 9 13


 #replicates arg1 arg2 times
rep(3, 50) # replicates 3 50 times
# this [1] shows the start of the vector
# [1] 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3
# this shows the count start for the second row; it starts with element 35
# [35] 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3
```

Accessing elements of a Vector
```r
w <- c("a", "b", "c", "d")
# chr [1:4] "a" "b" "c" "d"

# second element
w[2]
# [1] "b"

# everything but the first
w[-1]
# [1] "b" "c" "d"

# everything but the third in a variable 
v <- w[-3]
 # [1] "a" "b" "c"

# get specific elements, i.e., elements 1 - 3
w[1:3]
# [1] "a" "b" "c"

# get more specific elements, i.e., elements 1, 3, and 4
w[c(1, 3, 4)]
# [1] "a" "c" "d"

# get more specific exceptions, i.e., all elements except 2 & 3
w[c(-2, -3)]
# [1] "a" "d"

# get more general exceptions, i.e., all elements except 2-3
w[c(-2:-3)]
# [1] "a" "d" 
# bad example cause same output, but concept is True
```

Vectorized Operations
```r
# [Basic Loop Refresh]

# 5 element vector, each value a random normally distributed value
x <- rnorm(5)

# for loop for i in (5 element vector)
# in this loop, ~i~ is the given element
# R-specific
for(i in x){
  print(i)
}

# functionally equivalent but uses new vector to count elements
# in this loop, ~i~ is an numeric value 1 - 5
# conventional
for(i in 1:5){
  print(x[i])
}

# Comparing Vectorized and Non-Vectorized Functions

N <- 100
a <- rnorm(N)
b <- rnorm(N)

# vectorized approach
c <- a * b
c

# devectorized approach
# make an empty vector that is the same length as a and b
d <- rep(NA, N)

# for every value in a and b, multiply the elements 
# and insert into same location in d
for(i in 1:N){
  d[i] <- a[i] * b[i]
}
d
# this is slower and less clear/readable
```