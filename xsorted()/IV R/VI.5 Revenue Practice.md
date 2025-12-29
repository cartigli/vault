Practice:
You are given two vectors, one containing the years revenue and another containing the year's costs, by month. You need to find the profit, profit after taxes (at a 30% tax rate), profit margins (after-tax profit / revenue), and average for each month. Then, compare the average to each month and determine if each month was a good or bad month for profit (margins above or below the average). Also, find the highest and lowest profit margins from the year.

```r
# datatset
revenue <- c(14574.49, 7606.46, 8611.41, 9175.41, 8058.65, 8105.44, 11496.28, 9766.09, 10305.32, 14379.96, 10713.97, 15433.50)
expenses <- c(12051.82, 5695.07, 12319.20, 12089.72, 8658.57, 840.20, 3285.73, 5821.12, 6976.93, 16618.61, 10054.37, 3803.96)


profit <- revenue - expenses

after_taxes <- profit *.70

profit_margins <- after_taxes / revenue

mean <- mean(profit_margins)

best <- max(profit_margins)
worst <- min(profit_margins)

cnt <- 0

for(i in profit_margins){
  cnt <- cnt + 1
  x <- paste("month", cnt, ":")
  print(x)
    if(i==best){
      print("BEST month")
    }else if(i>mean){
    print("Good month")
    }else if(i==worst){
    print("WORST month")
  }else if(i<mean){
    print("Bad month")
  }
  print(i)
}
cnt <- 0
```