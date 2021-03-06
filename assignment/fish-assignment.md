
``` r
library(tidyverse)
```

# Unit 2: Fisheries Collapse Module

This module will focus on understanding and replicating fisheries stock
assessment data and fisheries collapse.

Instead of working with independent data.frames, we will be working with
a large relational database which contains many different tables of
different sizes and shapes, but that all all related to each other
through a series of different ids.

## The Database

We will use data from the [RAM Legacy Stock Assessment
Database](https://www.ramlegacy.org/database/)

# Exercise 1: Investigating the North-Atlantic Cod

Now we are ready to dive into our data. First, We seek to replicate the
following figure from the Millennium Ecosystem Assessment Project using
the RAM data.

![](http://espm-157.carlboettiger.info/img/cod.jpg)

## placeholder

``` r
mtcars %>% 
 ggplot(aes(disp, mpg)) + geom_point()
```

![](fish-assignment_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->

-----

# Exercise 2: Group Assignment

## Stock Collapses

We seek to replicate the temporal trend in stock declines shown in [Worm
et al 2006](http://doi.org/10.1126/science.1132294):

![](http://espm-157.carlboettiger.info/img/worm2006.jpg)
