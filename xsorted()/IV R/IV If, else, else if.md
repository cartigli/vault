```r
# ---- -2 ---- -1 ---- 0 ---- 1 ---- 2 ----

# rnorm(n, mean=0, std=1)) <- defaults of rnorm

rnorm(1) # makes a random normally distributed no.

rm(answer) # clears the answer variable's value
x <- rnorm(1)
x

# if(condition){action}
if(x>1){
  answer <- "Greater than 1"
}

rm(answer)
x <- rnorm(1)

if (x>1){
  answer <- "Greater than 1"
} else{
  if(x>=-1){
    answer <- "Between 1 and -1"
  } else{
    answer <- "Less than -1"
  }
}
# ^ nested if conditionals; chaining is usually preferred
rm(answer)
x <-rnorm(1)
if (x > 1){
  answer <- "Greater than 1"
} else if(x < -1){
  answer <- "Less than -1"
} else{
  answer <- "Between 1 and -1"
}
```

Normal Distribution / if else Practice
```r
# ---- -2 ---- -1 ---- 0 ---- 1 ---- 2 ----

# make the variables
p2 <- 0
p1 <- 0
n2 <- 0
n1 <- 0
np <- 0

# for i in range 1 to 1000
for(i in 1:1000){
     x <-rnorm(1)
     if(x >= 2){
          p2 <- p2 + 1
     } else if(x <= -2){
          n2 <- n2 + 1
     } else if(x >= 1){
          p1 <- p1 + 1
     } else if(x <= -1){
          n1 <- n1 + 1
     } else {
          np <- np + 1
     }
}

# get the total (dynamically; could have also set to 1000)
tot = p2 + p1 + n1 + n2 + np

# get individual percents
p2p <- p2 / tot
p1p <- p1 / tot
n1p <- n1 / tot
n2p <- n2 / tot

# add related values (by boundaries)
npp <- (np / tot)*100
b1 <- ((p1 + n1) / tot)*100
b2 <- ((p2 + n2) / tot)*100

# convert values to strings
inner <- toString(npp)
first <- toString(b1)
second <- toString(b2)

# format print statements
one <- paste("Percent beyond first standard deviation:", first)
two <- paste("Percent beyond first standard deviation:", second)
three <- paste("Percent within the first standard deviations:", inner)

# print formatted statements
print(three)
print(one)
print(two)
```

Example of the generated output: ('rscript script_name.r' is the bash command to run a script written in r)
~ % rscript x.r 
[1] "Percent within the first standard deviations: 68.185"
[1] "Percent beyond first standard deviation: 27.283"
[1] "Percent beyond first standard deviation: 4.532"
~ %

I couldn't figure out why the inner bounds and first bound lined up perfectly with the Normal Distribution while the outer second bounds were too high (by around 0.2%). This additional value is present because there is no third bound for the if else if block in the script above, so the 0.1% from the outer third bounds are either side are being added to the second bound value.

Revised:
```r
# ---- -2 ---- -1 ---- 0 ---- 1 ---- 2 ----

# make the variables
p3 <- 0
p2 <- 0
p1 <- 0
n3 <- 0
n2 <- 0
n1 <- 0
np <- 0

# for i in range 1 to 1000
for(i in 1:1000){
     x <-rnorm(1)
	 if(x >= 3){
		 p3 <- p3 + 1
	 }else if(x<=-3){
		 n3 <- n3 + 1
	 }else if(x >= 2){
          p2 <- p2 + 1
     } else if(x <= -2){
          n2 <- n2 + 1
     } else if(x >= 1){
          p1 <- p1 + 1
     } else if(x <= -1){
          n1 <- n1 + 1
     } else {
          np <- np + 1
     }
}

# get the total (dynamically; could have also set to 1000)
tot = p3 + p2 + p1 + n1 + n2 + n3 + np

# get individual percents
p3p <- p3 / tot
p2p <- p2 / tot
p1p <- p1 / tot
n1p <- n1 / tot
n2p <- n2 / tot
n3p <- n3 / tot

# add related values (by boundaries)
npp <- (np / tot)*100
b1 <- ((p1 + n1) / tot)*100
b2 <- ((p2 + n2) / tot)*100
b3 <- ((p3 + n3) / tot)*100

# convert values to strings
inner <- toString(npp)
first <- toString(b1)
second <- toString(b2)
third <- toString(b3)

# format print statements
one <- paste("Percent beyond first standard deviation:", first)
two <- paste("Percent beyond second standard deviation:", second)
three <- paste("Percent beyond third standard deviation:", third)
interior <- paste("Percent within the first standard deviations:", inner)


# print formatted statements
print(one)
print(two)
print(three)
print(interior)
```

Revised Output Example:
~ % rscript x.r
[1] "Percent within the first standard deviations: 68.9"
[1] "Percent beyond first standard deviation: 26.31"
[1] "Percent beyond second standard deviation: 4.59"
[1] "Percent beyond third standard deviation: 0.2"
~ %

*Law of Large Numbers*
As the range for the initial for conditional increases, the values produced by the script begin to lock around the normal distribution's distribution. Using a range over 10,000 forces the results to match the distribution nearly identically.