While Loops
```r
# abc is the indicator of whether to continue or break
while(abc){
  xyz # body of the loop
}

while(!FALSE){
  print("Hello")
} # INFINITE LOOP OF 'Hello's



counter <- 0

while(counter<10){
  print(counter)
  counter <- counter + 1
}
```

For Loops
```r

counter <- 0

while(counter<10){
  print("hello")
  counter <- counter + 1
}


# for i in range 1 to 5, iterate over the function's body
for(i in 1:5){
  print('hello, r')
}

x <- 1:5
x
# [1] 1 2 3 4 5 (the 1:5 vector)


y <- 7:12
y
# [1] 7 8 9 10 11 12

```