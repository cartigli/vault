```r
> matplot(t(FieldGoals), type="b", pch=15:18)
> matplot(t(FieldGoals), type="b", pch=15:18, col=c(1:4))
> matplot(t(FieldGoals), type="b", pch=15:18, col=c(1:4, 6))
> 
> matplot(t(FieldGoals), type="b", pch=15:18, col=c(1:4, 6))
> 
> legend("bottomleft", inset=0.01, legend=Players)
> legend("bottomleft", inset=0.01, legend=Players, col=c(1:4, 6))
> legend("bottomleft", inset=0.01, legend=Players, col=c(1:4, 6))
> 
> matplot(t(FieldGoals), type="b", pch=15:18, col=c(1:4, 6))
> legend("bottomleft", inset=0.01, legend=Players, col=c(1:4, 6))
> legend("bottomleft", inset=0.01, legend=Players, col=c(1:4, 6), pch=15:18, horiz=F)
> 
> matplot(t(FieldGoals), type="b", pch=15:18, col=c(1:4, 6))
> legend("bottomleft", inset=0.01, legend=Players, col=c(1:4, 6), pch=15:18, horiz=F)
> 
> # accuracy measurement; transpose both components of the division
> matplot(t(FieldGoals/FieldGoalAttempts), type="b", pch=15:18, col=c(1:4, 6))
> matplot(t(FieldGoals/FieldGoalAttempts), type="b", pch=15:18, col=c(1:4, 6))
```

Using subsets of Matrices
```r
matplot(t(MinutesPlayed), type="b", pch=15:18, col=c(1:4, 6))
legend("bottomleft", inset=0.01, legend=Players, pch=15:18, col=c(1:4,6))


data <- MinutesPlayed[1:4,]

matplot(t(data), type="b", pch=15:18, col=c(1:4, 6))
legend("bottomleft", inset=0.01, legend=Players[1:4], pch=15:18, col=c(1:4,6))


data1 <- MinutesPlayed[10,,drop=FALSE]

matplot(t(data1), type="b", pch=15:18, col=6)
legend("bottomleft", inset=0.01, legend=Players[10], pch=15:18, col=6)
```

Making Functions for Visualization:
```r
source("Untitled.R")

data1 <- MinutesPlayed[10,,drop=FALSE]

matplot(t(data1), type="b", pch=15:18, col=6)
legend("bottomleft", inset=0.01, legend=Players[10], pch=15:18, col=6)

# to make it into a function:

DwayneWade <- function(){
  # add the commands to the function body
  data1 <- MinutesPlayed[10,,drop=FALSE]
  matplot(t(data1), type="b", pch=15:18, col=6)
  legend("bottomleft", inset=0.01, legend=Players[10], pch=15:18, col=6)
}

# in environment, 'DwayneWade: function()' appears

DwayneWade()
# now this call alone slices the matrix, makes the graph, and adds a legend

# similarly, change the player by altering the Player legend & slice:
KobeBryant <- function(){
  # add the commands to the function body
  data1 <- MinutesPlayed[1,,drop=FALSE]
  matplot(t(data1), type="b", pch=15:18, col=6)
  legend("bottomleft", inset=0.01, legend=Players[1], pch=15:18, col=6)
}

KobeBryant()

# or top three of the matrix
TopThree <- function(){
  # add the commands to the function body
  data1 <- MinutesPlayed[1:3,,drop=FALSE]
  matplot(t(data1), type="b", pch=15:18, col=4:6)
  legend("bottomleft", inset=0.01, legend=Players[1:3], pch=15:18, col=4:6)
}

TopThree()

# Naturally, the progression of this is to add the indexes as arguments/parameters
Flexible <- function(rows){
  # add the commands to the function body
  data1 <- MinutesPlayed[rows,,drop=FALSE]
  matplot(t(data1), 
		  type="b", 
		  pch=15:18, 
		  col=c(1:4,6))
  legend("bottomleft", 
		  inset=0.01, 
		  legend=Players[rows], 
		  col=c(1:4,6), 
		  pch=15:18)
}

# graph the top 5 players
Flexible(1:5)

# graph the top three players
Flexible(1:3)

# graph the bottom three players
Flexible(8:10)

# graph the top player
Flexible(1)


# if we wanted the dataset to also be paramterized, we could do so like this:
Dynamic <- function(data, rows){
  # add the commands to the function body
  data1 <- data[rows,,drop=FALSE]
  matplot(t(data1), 
		  type="b", 
		  pch=15:18, 
		  col=c(1:4,6))
  legend("bottomleft", 
		  inset=0.01, 
		  legend=Players[rows], 
		  col=c(1:4,6), 
		  pch=15:18)
}

Dynamic(MinutesPlayed, 1:3)
Dynamic(FieldGoals, 1:10)
Dynamic(FieldGoals, 8:10)


# adding default values to the parameterized inputs:
Dynamite <- function(data=Salary, rows=1:10){
  # add the commands to the function body
  data1 <- data[rows,,drop=FALSE]
  matplot(t(data1), 
		  type="b", 
		  pch=15:18, 
		  col=c(1:4,6))
  legend("bottomleft", 
		  inset=0.01, 
		  legend=Players[rows], 
		  col=c(1:4,6), 
		  pch=15:18)
}

# now, without arguments supplied, the function defaults to Salary, rows 1:10
Dynamite()

# alt
Dynamite(Games/MinutesPlayed) # all players games per minute played
Dynamite(Games/MinutesPlayed, 3) # just the third player's values
```

*Sorry for the formatting discrepancies; some of this is done in the console, some in the terminal, and the majority in scripts while using R Studio. I do not enjoy this interface but I can't get plots to show otherwise.*

Bad vs. Good use of Visual Representation/Investigation of Data
```r
Dynamite(Salary)
Dynamite(Games)
Dynamite(Salary/Points) # REALLY bad
Dynamite(Salary/Games) # also REALLY bad

# this is better than the above because it considers goals per game,
# instead of pure games or pure salary, which don't account for injuries
Dynamite(FieldGoals/Games)
Dynamite(Points/Games)
Dynamite(MinutesPlayed/Games)

Dynamite(FieldGoals) # this is much less informative than...
Dynamite(FieldGoals/FieldGoalAttempts) # this (accuracy)

Dynamite(FieldGoals/MinutesPlayed) # (effectiveness)
```

Practice
```r
#Dear Student,
#
#Welcome to the dataset for the homework exercise.
#
#Instructions for this dataset:
# You have only been supplied vectors. You will need
# to create the matrices yourself.
# Matrices:
# - FreeThrows
# - FreeThrowAttempts
#
#Sincerely,
#Kirill Eremenko
#www.superdatascience.com

#Copyright: These datasets were prepared using publicly available data.
#           However, theses scripts are subject to Copyright Laws. 
#           If you wish to use these R scripts outside of the R Programming Course
#           by Kirill Eremenko, you may do so by referencing www.superdatascience.com in your work.

#Comments:
#Seasons are labeled based on the first year in the season
#E.g. the 2012-2013 season is preseneted as simply 2012

#Notes and Corrections to the data:
#Kevin Durant: 2006 - College Data Used
#Kevin Durant: 2005 - Proxied With 2006 Data
#Derrick Rose: 2012 - Did Not Play
#Derrick Rose: 2007 - College Data Used
#Derrick Rose: 2006 - Proxied With 2007 Data
#Derrick Rose: 2005 - Proxied With 2007 Data

#Seasons
Seasons <- c("2005","2006","2007","2008","2009","2010","2011","2012","2013","2014")

#Players
Players <- c("KobeBryant","JoeJohnson","LeBronJames","CarmeloAnthony","DwightHoward","ChrisBosh","ChrisPaul","KevinDurant","DerrickRose","DwayneWade")

#Free Throws
KobeBryant_FT <- c(696,667,623,483,439,483,381,525,18,196)
JoeJohnson_FT <- c(261,235,316,299,220,195,158,132,159,141)
LeBronJames_FT <- c(601,489,549,594,593,503,387,403,439,375)
CarmeloAnthony_FT <- c(573,459,464,371,508,507,295,425,459,189)
DwightHoward_FT <- c(356,390,529,504,483,546,281,355,349,143)
ChrisBosh_FT <- c(474,463,472,504,470,384,229,241,223,179)
ChrisPaul_FT <- c(394,292,332,455,161,337,260,286,295,289)
KevinDurant_FT <- c(209,209,391,452,756,594,431,679,703,146)
DerrickRose_FT <- c(146,146,146,197,259,476,194,0,27,152)
DwayneWade_FT <- c(629,432,354,590,534,494,235,308,189,284)
#Matrix
FreeThrows <- rbind(KobeBryant_FT, JoeJohnson_FT, LeBronJames_FT, CarmeloAnthony_FT, DwightHoward_FT, ChrisBosh_FT, ChrisPaul_FT, KevinDurant_FT, DerrickRose_FT, DwayneWade_FT)
#
# <put your code here>
#

#Free Throw Attempts
KobeBryant_FTA <- c(819,768,742,564,541,583,451,626,21,241)
JoeJohnson_FTA <- c(330,314,379,362,269,243,186,161,195,176)
LeBronJames_FTA <- c(814,701,771,762,773,663,502,535,585,528)
CarmeloAnthony_FTA <- c(709,568,590,468,612,605,367,512,541,237)
DwightHoward_FTA <- c(598,666,897,849,816,916,572,721,638,271)
ChrisBosh_FTA <- c(581,590,559,617,590,471,279,302,272,232)
ChrisPaul_FTA <- c(465,357,390,524,190,384,302,323,345,321)
KevinDurant_FTA <- c(256,256,448,524,840,675,501,750,805,171)
DerrickRose_FTA <- c(205,205,205,250,338,555,239,0,32,187)
DwayneWade_FTA <- c(803,535,467,771,702,652,297,425,258,370)
#Matrix
FreeThrowAttempts <- rbind(KobeBryant_FTA, JoeJohnson_FTA, LeBronJames_FTA, CarmeloAnthony_FTA, DwightHoward_FTA, ChrisBosh_FTA, ChrisPaul_FTA, KevinDurant_FTA, DerrickRose_FTA, DwayneWade_FTA)
#
# <put your code here>
#

FreeThrows
FreeThrowAttempts

visualize <- function(data, rows=1:10){
  info <- data[rows,,drop=FALSE]
  matplot(info, 
		  type="b", 
		  pch=15:18, 
		  col=c(1:4,6))
  legend("bottomleft", 
		  inset=0.01, 
		  pch=15:18, 
		  legend=Players, 
		  col=c(1:4,6))
}

visualize(FreeThrows)
visualize(FreeThrows/FreeThrowAttempts)

visualize(FreeThrows/FreeThrowAttempts, 6:10)
```

Homework (chopped)
```r
# ---- Homework ----

newData <- read.csv("S5-Homework-Data.csv", stringsAsFactors=TRUE)
head(newData)
tail(newData)

data1960 <- newData[newData$Year == 1960,]
head(data1960)

data2013 <- newData[newData$Year == 2013,]
head(data2013)

qplot(data=data2013, x=Region, y=Fertility.Rate, color=Region, size=I(2))
qplot(data=data1960, x=Region, y=Fertility.Rate, color=Region, size=I(2))
```