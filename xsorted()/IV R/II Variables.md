Variable Types
```r
# integer ('L' is required to make it an integer)
x <- 2L
typeof(x)

# double (L not used)
y <- 2.5
typeof(y)

z <- 2
typeof(z)
# this is also a double!

# complex
a <- 4 + 2i
typeof(a)

# character
b <- "worldwide"
typeof(b)

# logical
c1 <- T
typeof(c1)

d <- FALSE
typeof(d)
```

Using Variables:
```r
A <- 10
B <- 5

c <- A + B
c <- A+B
# to get the value of c output in the console, run just the object's name as a command:
c

var1 <- 2.5
var2 <- 4

# division
var3 <- var1 / var2
var3 # [1] 0.625
typeof(var3) # [1] "double"

# multiplication
var4 <- var1 * var2
var4 # [1] 10
typeof(var4) # [1] "double"

# square root
result <- sqrt(var1)
result # [1] 1.581139
typeof(result) # [1] "double"

greeting <- "Hello,"
name <- "Joe"

# combine two strings with 'paste(str1, str2)'
message <- paste(greeting, name)
message
```

Logical Operators
```r
# logical
# TRUE T
# FALSE F

4 < 5
[1] TRUE
10 > 100
[1] FALSE

4 = 5
Error in 4 = 5 : invalid (do_set) left-hand side to assignment
4 == 5
[1] FALSE

# ==
# !=
# equal/not equal

# <
# >
# <=
# >=

# !
# NOT

# /
# OR

# &
# AND

# isTRUE(x)
# checks if x is TRUE


results <- 4 < 5

results
[1] TRUE
# results stores the logical operators result

typeof(results)
[1] "logical"


# NOT
result1 <- !TRUE

result1
[1] FALSE
# FALSE == NOT TRUE

result2 <- !(4 < 5)

result2
[1] FALSE


# OR, AND
results | result2
[1] TRUE
# either results or result2 is TRUE

results & result2
[1] FALSE
# both results and result2 is TRUE is FALSE

isTRUE(result2)
[1] FALSE
isTRUE(results)
[1] TRUE
```