# Reproducible Research: Peer Assessment 1
## [github.com/l0neJT](http://www.github.com/l0neJT)
## 9 June 2014

### Introduction
This assignment demonstrates the use of [R Markdown](http://rmarkdown.rstudio.com/) in conjunction with the [knitr package](http://cran.r-project.org/web/packages/knitr/index.html) to produce literate code. Forked from [rdpeng/RepData_PeerAssessment1](http://github.com/rdpeng/RepData_PeerAssessment1).

### Loading and preprocessing the data
 1. Load packages [plyr](http://cran.r-project.org/web/packages/plyr/index.html) and [ggplot2](http://cran.r-project.org/web/packages/ggplot2/index.html)

```r
library(plyr)
library(ggplot2)
```
 2. Load data from file activity.csv

```r
dat <- read.csv("./data/activity.csv")
```
 3. Transform the 'date' column from factor into date

```r
dat <- transform(dat, date = as.Date(date, format = "%Y-%m-%d"))
str(dat)
```

```
## 'data.frame':	17568 obs. of  3 variables:
##  $ steps   : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ date    : Date, format: "2012-10-01" "2012-10-01" ...
##  $ interval: int  0 5 10 15 20 25 30 35 40 45 ...
```

### What is mean total number of steps taken per day?
1. Summarise steps by date (excluding NAs)

```r
stepsNoNA <- ddply(dat[!is.na(dat$steps), ], "date", summarise, steps = sum(steps))
```
2. Chart steps by date as a bar plot with mean line

```r
plot <- qplot(date, steps, data = stepsNoNA, geom = "bar", stat = "identity")
plot + geom_hline(yintercept = mean(stepsNoNA$steps), color = "red", size = 2)
```

![plot of chunk histStepsNoNA](figure/histStepsNoNA.png) 

```r
# Add a lavel to line
```

### What is the average daily activity pattern?

### Imputing missing values

### Are there differences in activity patterns between weekdays and weekends?
