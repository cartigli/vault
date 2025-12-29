```r
data <- read.csv("S6-Movie-Ratings.csv")

# ---- Preparing Data ----

head(data)
tail(data)

nrow(data)
# [1] 562
ncol(data)
# [1] 6

str(data)
summary(data)

colnames(data) <- c("Film", "Genre", "Critic.Rating", "Audience.Rating", "Budget", "Year")
head(data)

data$Year <- factor(data$Year)
head(data)

summary(data)

# ---- Using ggplot2() ----

library(ggplot2)

# add the data
ggplot(data=data)

# add aesthetics
ggplot(data=data, aes(x=Critic.Rating, y=Audience.Rating))

# add a minimal geometry, just to obtain visuals
ggplot(data=data, aes(x=Critic.Rating, y=Audience.Rating)) +
      geom_point()

# add coloring
ggplot(data=data, aes(x=Critic.Rating, y=Audience.Rating,
                      color=Genre)) +
  geom_point()

# add size (ggplot will warn about using size with a discrete variable)
ggplot(data=data, aes(x=Critic.Rating, y=Audience.Rating,
                      color=Genre,
                      size=Genre)) +
  geom_point()

# add size apropriately
ggplot(data=data, aes(x=Critic.Rating, y=Audience.Rating,
                      color=Genre,
                      size=Budget)) +
  geom_point()


# ---- Plotting with Layers ----

# create an object with the plot
plot <- ggplot(data=data, aes(x=Critic.Rating, y=Audience.Rating,
                              color=Genre,
                              size=Budget))

plot # blank; no geometry, so...

# add it on top of the 'plot' layer
geo_plot <- plot + geom_point()

geo_plot

# ---- Overriding Aesthetics ----

plot + geom_point()

# example 1
# override the plot object's size aesthetic with geom_point
plot + geom_point(aes(size=Critic.Rating))

# example 2
# overriding the plot object's color aesthetic with geom_point
plot + geom_point(aes(color=Budget))

# example 3
# overriding the plot object's x/y aesthetics
plot + geom_point(aes(x=Budget)) +
  xlab("Budget in Millions ($)") # x-axis title

# **None of the overrides above modify the original plot object**
# *The above all use 'mapping' to override the aesthetic.
# Below uses 'setting' instead of mapping.*

# Imagine we used lines + points
plot + geom_line() + geom_point()# basically useless

# 'setting' the size (rather than 'mapping' the size)
plot + geom_line(size=1) + geom_point()

# mapping the size - didn't seem to have an effect
plot + geom_line(aes(size=0.1)) + geom_point()
```

Example 3's Plot:
![[Pasted image 20251228112748.png]]

Mapping vs. Setting
```r
# Non-configured
r <- ggplot(data=data, aes(x=Critic.Rating, y=Audience.Rating))
r + geom_point()

# Mapping (what we have already done)
r + geom_point(aes(color=Genre))

# Setting
r + geom_point(color=Genre) # ERROR
r + geom_point(color="DarkGreen") # every point is now green

r + geom_point(aes(size=Budget))
r + geom_point(size=Budget) # ERROR
r + geom_point(size=1) # sets size for ALL points
```

Histograms and Density Charts
```r
# Histograms
s <- ggplot(data=data, aes(x=Budget))
s + geom_histogram(binwidth=10) # bar width of histogram

# 'set' the color
s + geom_histogram(binwidth=10, fill="Green")

# map the color
s + geom_histogram(binwidth=10, aes(fill=Genre))

# add a colored border (to mapped colors)
s + geom_histogram(binwidth=10, aes(fill=Genre), color="Black")

# Density Charts
s + geom_density()

# add coloring by Genre
s + geom_density(aes(fill=Genre))

# make the layers stack appropriately
s + geom_density(aes(fill=Genre), position="stack")
# now each layer is clearly visible
```