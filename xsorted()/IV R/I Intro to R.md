Installed r from their site; downloaded and installed R-Studio but god damn it is awful. Will remove asap.

Allows terminal like interactions with a more refined UI. Data, packages, variables are all clearly displayed in the UI.

We downloaded an example set from their site named 'diamond price' and ran a few simple commands to format the output and generate a visual representation of the data. 

We made a single function and iteratively added complexity to it. Below are the final 2-3 editions.

```r
# let's you choose from the finder ui
mydata <- read.csv(file.choose())

# install the graph tool/library
install.packages("ggplot2")
# note: this installs but does not load the ggplot2 lib. We manually selected it in RStudio, but it is normally done with library(ggplot2)
# i was unloading this library when the command to do so appeared in the console:
detach("package:ggplot2", unload = TRUE) # unchecks the installed library

# aes is aesthetics; non-computation specifications
ggplot(data=mydata,
       aes(x=carat,
           y=price,
           colour=clarity
           )
       ) +
  geom_point(alpha=0.1)

# like a list slice for the x variables; hard maximum at 2,5
ggplot(data=mydata[mydata$carat<2.5,],
       aes(x=carat,
           y=price,
           colour=clarity
           )
       ) +
  geom_point(alpha=0.1) +
  geom_smooth() # this smooths the points and creates trend lines from the scatter plot
```