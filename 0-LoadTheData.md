---
title: "Task0-LoadTheData"
author: "Grace Pehl, PhD"
date: "October 10, 2015"
output: html_document
---




```r
library(R.utils)
```

```
## Loading required package: R.oo
## Loading required package: R.methodsS3
## R.methodsS3 v1.7.0 (2015-02-19) successfully loaded. See ?R.methodsS3 for help.
## R.oo v1.19.0 (2015-02-27) successfully loaded. See ?R.oo for help.
## 
## Attaching package: 'R.oo'
## 
## The following objects are masked from 'package:methods':
## 
##     getClasses, getMethods
## 
## The following objects are masked from 'package:base':
## 
##     attach, detach, gc, load, save
## 
## R.utils v2.1.0 (2015-05-27) successfully loaded. See ?R.utils for help.
## 
## Attaching package: 'R.utils'
## 
## The following object is masked from 'package:jsonlite':
## 
##     validate
## 
## The following object is masked from 'package:utils':
## 
##     timestamp
## 
## The following objects are masked from 'package:base':
## 
##     cat, commandArgs, getOption, inherits, isOpen, parse, warnings
```

```r
reviewfile = 'yelp_academic_dataset_review.json'
n_reviews <- countLines(reviewfile) # 1,569,264 entries
library(readr)
# Hadley Wickham's readr package saved hours of loading time
t0 <- proc.time()
reviews <- read_lines(reviewfile, n_max = n_reviews) # char vector
proc.time() - t0 # only 21s!!!
```

```
##    user  system elapsed 
##   18.68    0.98   21.30
```

```r
reviews <- sample(reviews, size = 0.1 * n_reviews) # subset
# pseudo-JSON, each entry is JSON, but entries aren't linked
# separate entries by commas and surround file with brackets
reviews <- paste(reviews, collapse = ", ")
reviews <- paste('[', reviews, ']', sep = '')
library(jsonlite)
reviews <- fromJSON(reviews) # dataframe
proc.time() - t0
```

```
##    user  system elapsed 
##   31.17    1.80   35.66
```

```r
saveRDS(reviews, file = 'reviews1.rds') #save the dataframe
```


```r
bizfile = 'yelp_academic_dataset_business.json'
n_biz <- countLines(bizfile)
t1 <- proc.time()
businesses <- read_lines(bizfile, n_max = n_biz)
proc.time() - t1
```

```
##    user  system elapsed 
##    0.28    0.00    0.31
```

```r
businesses <- paste(businesses, collapse = ", ")
businesses <- paste('[', businesses, ']', sep = '')
businesses <- fromJSON(businesses)
proc.time() - t1
```

```
##    user  system elapsed 
##   44.33    0.33   46.79
```

```r
saveRDS(businesses, file = 'business1.rds')
```


```r
tipfile = 'yelp_academic_dataset_tip.json'
n_tip <- countLines(tipfile)
t1 <- proc.time()
tips <- read_lines(tipfile, n_max = n_tip)
proc.time() - t1
```

```
##    user  system elapsed 
##    0.83    0.02    0.82
```

```r
tips <- paste(tips, collapse = ", ")
tips <- paste('[', tips, ']', sep = '')
tips <- fromJSON(tips)
proc.time() - t1
```

```
##    user  system elapsed 
##   18.00    0.88   19.78
```

```r
saveRDS(tips, file = 'tips1.rds')
```


```r
userfile = 'yelp_academic_dataset_user.json'
n_user <- countLines(userfile)
t1 <- proc.time()
users <- read_lines(userfile, n_max = n_user)
proc.time() - t1
```

```
##    user  system elapsed 
##    1.08    0.04    1.14
```

```r
users <- paste(users, collapse = ", ")
users <- paste('[', users, ']', sep = '')
users <- fromJSON(users)
proc.time() - t1
```

```
##    user  system elapsed 
## 2708.94  449.22 3450.71
```

```r
saveRDS(users, file = 'users1.rds')
```


