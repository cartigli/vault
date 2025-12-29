*In the terminal, the same '?[function]' help menu is savailble*
*It is displayed line by line and scrollable with Return, escape with 'q'.


```r
x <- 1

is.numeric()
is.integer()
is.double()
is.character()
isTRUE()
isFASLE()
typeof()

rnorm()
c()
seq()
rep()

print()
paste()

sqrt()

# the help indicator
# ?
?rnorm()
?sqrt()
?c()
?paste()
?seq()
# alteast in R-Studio, these commands opens a
# help-windows with function params and abilities

# rnorm() non-default example
y <- rnorm(n=7, sd=3)
y
# [1] -2.9220488 -1.9005030  1.0661637  3.4236929  0.4987541 -5.1485322
# [7] -1.8759373

# seq() non-default example
z <- seq(4, 5, 2)
z
# [1] 4

# OR

z <- seq(from=4, to=5, by=2)
z
# [1] 4
# functionally equivalent whether you name the key values or not

?rep()

c <- rep(5:6, 10)
c
# (5, 6) repeating 10 times

# rep() non-default example
a <- rep(5:6, each=10)
a
# 5 ten times, then 6 ten times
```

Packages
```r
# adding a package (installing)
library(ggplot2)

# unload a package
detahc("package:ggplot2", unload = TRUE)

# delete a package
remove.packages("ggplot2")


# install a package
install.packages("ggplot2")

?qplot()
# causes an error becasue we don't have this library yet
?ggplot()
# causes same error

# activate the package
library(ggplot2)
# or library("ggplot2")

# now these commands correctly retrieve their respective help menus
?qplot()
?ggplot()
```