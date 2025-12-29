This is strange to me, but you index matrices using the y-axis before the x-axis. The rows, in descending order, are indexed as: m[1,], m[2,], m[3,]. These rows' values are referenced as the other coordinate pair of their given row: m[1, 2] = 9, m[2, 4] = 5, m[2,1] = 2

| m[1,1] | m[1,2] | m[1,3] | m[1,4] |
| ------ | ------ | ------ | ------ |
| m[2,1] | m[2,2] | m[2,3] | m[2,4] |
| m[3,1] | m[3,2] | m[3,3] | m[3,4] |

Making Matrices
```r
a <- c(1, 2, 3)
b <- c(4, 5, 6)
c <- c(7, 8, 9)
m <- rbind(a, b, c)
m
m[1,1]
m[3,2]

m1 <- matrix(m, 3, 3)
m1

new_data <- 1:48
m2 <- matrix(new_data, 6, 8)
m2

m3 <- matrix(new_data, 6, 8, byrow=TRUE)
m3

m4 <- matrix(new_data, 6, 8, byrow=F)
m4
```

An example of a matrix output by R; it already points its indeces out:
 -> m4
       [,1]  [,2]  [,3]  [,4]  [,5]  [,6]  [,7]  [,8]
 [1,]  1     7    13    19    25    31    37    43
 [2,]  2     8    14    20    26    32    38    44
 [3,]  3     9    15    21    27    33    39    45
 [4,]  4    10    16    22    28    34    40    46
 [5,]  5    11    17    23    29    35    41    47
 [6,]  6    12    18    24    30    36    42    48

 Named Vectors get their elements labeled. If the vector V has its seond element is named 'a', it could be referenced as either V["a"] AND/OR V[2]. Both are acceptable with named vectors, the original indexing is not forgotten.

 Ok, here's the key. I don't know how I did not see this before but rbind == row_bind and cbind == column_bind. So if you want 
 the vectors to be rows, use rbind and the first element of each vertex will be the first element of each row. Conversely, if you 
 want the vectors as columns, use cbind and the first element of each vertex will be the first element of each column.

 Back to Named Vectors
 ```r
> Rachel <- 1:5
> 
> names_ <- c("a", "b", "c", "d", "e")
> names(Rachel) <- names_
> 
> Rachel[a]
Error: object 'a' not found
> Rachel["a"]
a 
1 
> Rachel["c"]
c 
3 
> 
> Rachel
a b c d e 
1 2 3 4 5 
> names(Rachel)
[1] "a" "b" "c" "d" "e"
> 
> # clear the names 
> names(Rachel) <- NULL
> 
> Rachel
[1] 1 2 3 4 5
> names(Rachel)
NULL
> 
 ```

Names Matrices
```r
> v <- c("xX", "yY", "zZ")
> m <- matrix(rep(v, 3), 3, 3)
> m
     [,1] [,2] [,3]
[1,] "xX" "xX" "xX"
[2,] "yY" "yY" "yY"
[3,] "zZ" "zZ" "zZ"
> 
> names(m)
NULL
> rownames(m)
NULL
> rownames(m) <- c("Who", "goes", "there")
> colnames(m) <- c("Its", "the", "Kid")
> m
      Its the  Kid 
Who   "xX" "xX" "xX"
goes  "yY" "yY" "yY"
there "zZ" "zZ" "zZ"
> 
> colnames(m) <- NULL
> m
      [,1] [,2] [,3]
Who   "xX" "xX" "xX"
goes  "yY" "yY" "yY"
there "zZ" "zZ" "zZ"
> 
> colnames(m) <- c("Its", "the", "Kid")
> 
> m["goes","Kid"]
[1] "yY"
> m["goes","Kid"] <- 4
> 
> m["goes","Kid"]
[1] "4"
> m
      Its the  Kid 
Who   "xX" "xX" "xX"
goes  "yY" "yY" "4" 
there "zZ" "zZ" "zZ"
> 
> rownames(m)
[1] "Who"   "goes"  "there"
> 
> colnames(m)
[1] "It's" "the"  "Kid" 
> 
```

Submatrices 
```r
source("Untitled.R")
Games

Players
Salary

x <- Salary[1:3,6:10] # columns 1-3, rows 6-10

y <- Salary[c(1, 10),] # first row, last row (highest - lowest salaries)

z <- Salary[,c("2008", "2009")] # all salaries from 2008 & 2009

# ^ these subsets all worked out to be matrices
is.matrix(x)
# [1] TRUE

is.matrix(y)
# [1] TRUE

is.matrix(z)
# [1] TRUE

# to take a vector would mean to take a single dimension of a matrix
a <- Salary[1,]
a
#     2005     2006     2007     2008     2009     2010 
# 15946875 17718750 19490625 21262500 23034375 24806250 
# 2011     2012     2013     2014 
# 25244493 27849149 30453805 23500000

is.matrix(a)
# [1] FALSE

is.vector(a)
# [1] TRUE

# selecting a single item has the same effect
b <- Salary[1,7]
b
# [1] 25244493

is.vector(b)
# [1] TRUE

# this is due to the drop in the '[,]' selection that defaults to TRUE

k <- Salary[1,,drop=FALSE]
is.vector(k)
# [1] FALSE

is.matrix(k)
# [1] TRUE

k
#              2005     2006     2007     2008     2009     2010     2011     2012     2013     2014
# KobeBryant 15946875 17718750 19490625 21262500 23034375 24806250 25244493 27849149 30453805 23500000

# now this is in a matrix
# the same is possible with a single element
l <- Salary[1,7,drop=FALSE]
l
#              2011
# KobeBryant 25244493

is.matrix(l)
# [1] TRUE
```

