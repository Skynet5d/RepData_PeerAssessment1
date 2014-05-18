# Reproducible Research: Peer Assessment 1


## Loading and preprocessing the data

```r
repdata <- read.csv("./activity/activity.csv", header = TRUE)
str(repdata)
```

```
## 'data.frame':	17568 obs. of  3 variables:
##  $ steps   : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ date    : Factor w/ 61 levels "2012-10-01","2012-10-02",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ interval: int  0 5 10 15 20 25 30 35 40 45 ...
```



## What is mean total number of steps taken per day?

```r
dailysteps <- tapply(repdata$steps, repdata$date, sum, na.rm = FALSE)
hist(dailysteps, breaks = 62, xlab = "Total Daily Steps", main = paste("Histogram of Total Daily Steps"), 
    )
```

![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-2.png) 

The mean of daily total number of steps is

```r
mean(dailysteps)
```

```
## [1] NA
```


The median of daily total number of steps is

```r
median(dailysteps)
```

```
## <NA> 
##   NA
```


## What is the average daily activity pattern?



## Imputing missing values
The total number of missing values in the dataset is :

```r
length(which(is.na(repdata$steps)))
```

```
## [1] 2304
```


The filling strategy consists in replacing NAs values by daily mean of steps.
Here below the new dataset filled with this strategy :

```r
newrepdata <- repdata
newrepdata$avg <- ave(repdata$steps, repdata$date, na.rm = TRUE)
newrepdata$steps[!is.na(newrepdata$steps)] <- newrepdata$avg[!is.na(newrepdata$steps)]
```

Here the new histogramm :

```r
dailysteps <- tapply(newrepdata$steps, newrepdata$date, sum, na.rm = TRUE)
hist(dailysteps, breaks = 62, xlab = "Total Daily Steps", main = paste("Histogram of Total Daily Steps"), 
    )
```

![plot of chunk unnamed-chunk-7](figure/unnamed-chunk-7.png) 

The new mean of daily total number of steps is

```r
mean(dailysteps)
```

```
## [1] 9354
```


The new median of daily total number of steps is

```r
median(dailysteps)
```

```
## [1] 10395
```

```r

## Are there differences in activity patterns between weekdays and weekends?
```
