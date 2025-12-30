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

Histogram:
![[histogram.png]]

Density Chart:
![[density.png]]

Statistical Transformations (Layering)
```r

# ---- Statistical Transformations ----

?geom_smooth
# aids the eye in seeing patterns when overplotting is present

u <- ggplot(data=data, aes(x=Critic.Rating, y=Audience.Rating,
                           color=Genre,
                           alpha=0.2)) # slightly fade the points

u + geom_point()

u + geom_point() + geom_smooth()

u + geom_smooth()

u + geom_smooth(fill=NA)

u + geom_point() + geom_smooth(fill=NA)


# ---- Boxplots ----

# categorical x-values needed
v <- ggplot(data=data, aes(x=Genre, y=Critic.Rating,
                           color=Genre))

v + geom_boxplot()

v + geom_boxplot(size=1.2)

# useless/non-informative
v + geom_boxplot() + geom_point() 

# workaround for relevancy:
v + geom_boxplot() + geom_jitter()
# visually shows variation/outliers

# or add boxplots on top of points & introduce transparency
v + geom_jitter() + geom_boxplot(alpha=0.6)
```

Smoothed Scatter Plot:
![[smoothed.png]]

Fabricated Boxplot:
![[boxplot.png]]


Facets & Zooming/Cropping
```r
# ---- Facets ----

v <- ggplot(data=data, aes(x=Budget))

# illegible
v + geom_histogram(binwidth = 10)

# legible
v + geom_histogram(binwidth=10, aes(fill=Genre))

# clean
v + geom_histogram(binwidth=10, aes(fill=Genre),
                   color="Black")

# all the genres are bundled in one histogram
# facets allows us to make more indepent charts

# rows of histograms by Genre
v + geom_histogram(binwidth=10, aes(fill=Genre),
                   color="Black") +
  facet_grid(Genre~.)

# columns of histograms by Genre
v + geom_histogram(binwidth=10, aes(fill=Genre),
                   color="Black") +
  facet_grid(.~Genre)
# ^ each histogram is scaled on the same value; to do otherwise:

v + geom_histogram(binwidth=10, aes(fill=Genre),
                   color="Black") +
  facet_grid(Genre~.,scales="free")
# ^ each histogram is scaled by their respective ranges independently

# facets with scatter plots
w <- ggplot(data=data, aes(x=Critic.Rating, y=Audience.Rating,
                           color=Genre))

w + geom_point() # generic

w + geom_point() + facet_grid(Genre~.)
# OR
w + geom_point() + facet_grid(.~Year)
# AND
w + geom_point() + facet_grid(Genre~Year)
# bada fricking boom

w + geom_point() + 
  geom_smooth() +
  facet_grid(Genre~Year)

w + geom_point() + 
  geom_smooth(fill=NA) +
  facet_grid(Genre~Year)

w + geom_point(aes(size=Budget)) + 
  geom_smooth() +
  facet_grid(Genre~Year)

# --- Coordinates/Cropping/Zooming ----

w <- ggplot(data=data, aes(x=Critic.Rating, y=Audience.Rating,
                           size=Budget,
                           color=Genre))

w + geom_point()

# cropped view of points within x(50-100) & y(0-100)
w + geom_point() + 
  xlim(50,100)
# WARNING: 304 rows removed (good)

# cropped view of points within x(50-100) & y(50-100)
w + geom_point() +
  xlim(50,100) +
  ylim(50,100)
# WARNING: 335 rows removed (still good)

# ^ this is like a crop more than a zoom
# it works really well for scatter plots since they are defined by their x & y axis
# histograms, for example, are adversely affected by the same transformation

v <- ggplot(data=data, aes(x=Budget))

# normal/uncropped
v + geom_histogram(binwidth=10, aes(fill=Genre),
                   color="Black")

v + geom_histogram(binwidth=10, aes(fill=Genre),
                   color="Black") +
  ylim(0,50)
# instead of zooming, the crop simply removed values outside the range, distorting the histogram

# actually zoom (without cropping)
# use Cartesian coordinates (Quadrants I, II, III, & IV on the x/y axis)

v + geom_histogram(binwidth=10, aes(fill=Genre),
                   color="Black") +
  coord_cartesian(xlim=c(0,50), ylim=c(0,50))
# zoom without distorting values!

v + geom_histogram(binwidth=10, aes(fill=Genre),
                   color="Black") +
  coord_cartesian(ylim=c(0,50))
# original data still exists, but is not shown instead of being removed

# apply to faceted scatter plots from earlier:
# original faceted scatter plots:

# facets with scatter plots
w + geom_point(aes(size=Budget)) + 
  geom_smooth() +
  facet_grid(Genre~Year)

# zoomed in (no y-axis values below 0)
w + geom_point(aes(size=Budget), alpha=0.5) + 
  geom_smooth() +
  facet_grid(Genre~Year) +
  coord_cartesian(ylim=c(0,100))
# I won't lie, this is cool
```

Faceted, Zoomed & Smoothed Scatter Plot:
![[faceted_zoomed_smoothed_scatter.png]]

Themes (non-data ink)
```r
v <- ggplot(data=data, aes(x=Budget))

# add this layer to a new object: x
x <- v + geom_histogram(binwidth=10, aes(fill=Genre),
                   color="Black")

# now, x has layers one and two inside it
x # normal histogram

# label axis
x + xlab("Budget") # "Budget appears on the x-axis

# labeling axis/altering ticks
x + xlab("Money Axis") + 
  ylab("Num. of Movies") + 
  theme(axis.title.x=element_text(color="DarkGreen", size=10),
        axis.title.y=element_text(color="Red", size=10),
        axis.text.x=element_text(size=5), # edit tick mark sizes
        axis.text.y=element_text(size=5)) # both axis

# alter/set the legend's theme
x + xlab("Money Axis") + 
  ylab("Num. of Movies") + 
  theme(axis.title.x=element_text(color="DarkGreen", size=10),
        axis.title.y=element_text(color="Red", size=10),
        axis.text.x=element_text(size=5),
        axis.text.y=element_text(size=5),
        
        legend.title=element_text(size=10),
        legend.text=element_text(size=5))

# alter the legend's position
x + xlab("Money Axis") + 
  ylab("Num. of Movies") + 
  theme(axis.title.x=element_text(color="DarkGreen", size=10),
        axis.title.y=element_text(color="Red", size=10),
        axis.text.x=element_text(size=5),
        axis.text.y=element_text(size=5),
        
        legend.title=element_text(size=10),
        legend.text=element_text(size=5),
        legend.position=c(1,1)) # this alone skews the position

# correct position
x + xlab("Money Axis") + 
  ylab("Num. of Movies") + 
  theme(axis.title.x=element_text(color="DarkGreen", size=10),
        axis.title.y=element_text(color="Red", size=10),
        axis.text.x=element_text(size=5),
        axis.text.y=element_text(size=5),
        
        legend.title=element_text(size=10),
        legend.text=element_text(size=5),
        legend.position=c(1,1),
        legend.justification = c(1,1)) # this adjusts it correctly

# add a title
x + xlab("Money Axis") + 
  ylab("Num. of Movies") + 
  ggtitle("Movie Budget Distribution") +
  theme(axis.title.x=element_text(color="DarkGreen", size=10),
        axis.title.y=element_text(color="Red", size=10),
        axis.text.x=element_text(size=5),
        axis.text.y=element_text(size=5),
        
        legend.title=element_text(size=7),
        legend.text=element_text(size=7),
        legend.position=c(1,1),
        legend.justification = c(1,1))

# alter title
x + xlab("Money Axis") + 
  ylab("Num. of Movies") + 
  ggtitle("Movie Budget Distribution") +
  theme(axis.title.x=element_text(color="DarkGreen", size=10),
        axis.title.y=element_text(color="Red", size=10),
        axis.text.x=element_text(size=5),
        axis.text.y=element_text(size=5),
        
        legend.title=element_text(size=7),
        legend.text=element_text(size=7),
        legend.position=c(1,1),
        legend.justification = c(1,1),
        
        plot.title = element_text(size=10,
                                  color="Black",
                                  family="Courier"))
```

'Themed' Histogram
![[Refined_histogram_w.Titles.png]]