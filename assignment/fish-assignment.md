
# Unit 3: Fisheries Collapse Module

This module will focus on understanding and replicating fisheries stock
assessment data and fisheries collapse.

Instead of working with independent dataframes, we will be working with
a large relational database which contains many different tables of
different sizes and shapes, but that all all related to eachother
through a series of different ids.

## The Database

We will use data from the [RAM Legacy Stock Assessment
Database](https://doi.org/10.5281/zenodo.2542918)

First, load in the necessary libraries. Note that this time we need a
package we haven’t used before `readxl`. This package is useful for
reading in .xls or .xlsx files. As always if you want more info on a
package run `?readxl` after loading it.

``` r
library("tidyverse")
library("readxl")
```

## Reading in the tables

First thing, you are going to need to download and unzip the files.
Although you don’t need to do this step more than once, Travis will need
this code to be able to reproduce you work successfully, unless you
choose to push the datafiles up to git.

``` r
excel_version <- "RLSADB v4.44/DB Files With Assessment Data/RLSADB v4.44 (assessment data only).xlsx"
if(!file.exists(excel_version)){
  download.file("https://zenodo.org/record/2542919/files/RLSADB%20v4.44.zip?download=1",
                "ramlegacy.zip")
unzip("ramlegacy.zip") 
}
```

``` r
sheets <- readxl::excel_sheets(excel_version) #use the readxl package to identify sheet names 
ram <- lapply(sheets, readxl::read_excel, path = excel_version)  #read the data from all 3 sheets into a list
names(ram) <- sheets # give the list of datatables their assigned sheet names

## check your names
names(ram)
```

    ##  [1] "area"                         "assessment"                  
    ##  [3] "assessmethod"                 "assessor"                    
    ##  [5] "biometrics"                   "bioparams"                   
    ##  [7] "bioparams_assessments_views"  "bioparams_ids_views"         
    ##  [9] "bioparams_notes_views"        "bioparams_sources_views"     
    ## [11] "bioparams_units_views"        "bioparams_values_views"      
    ## [13] "management"                   "stock"                       
    ## [15] "taxonomy"                     "timeseries"                  
    ## [17] "timeseries_assessments_views" "timeseries_ids_views"        
    ## [19] "timeseries_notes_views"       "timeseries_sources_views"    
    ## [21] "timeseries_units_views"       "timeseries_values_views"     
    ## [23] "timeseries_years_views"       "tsmetrics"

``` r
## check your data
head(ram$area)
```

    ## # A tibble: 6 x 6
    ##   country  areatype areacode areaname             alternateareaname areaid      
    ##   <chr>    <chr>    <chr>    <chr>                <chr>             <chr>       
    ## 1 Argenti… CFP      ARG-N    Northern Argentina   NA                Argentina-C…
    ## 2 Argenti… CFP      ARG-S    Southern Argentina   NA                Argentina-C…
    ## 3 Austral… AFMA     CASCADE  Cascade Plateau      NA                Australia-A…
    ## 4 Austral… AFMA     EAUS     Eastern Australia    NA                Australia-A…
    ## 5 Austral… AFMA     ESE      Eastern half of Sou… NA                Australia-A…
    ## 6 Austral… AFMA     GAB      Great Australian Bi… NA                Australia-A…

Side Note: You may notice the `lapply` function above. This function
applies a given function (in this case “read\_excel”) to all elements in
a vector or list. This is the same as writing out read\_excel for all
the sheets contained in our file, or writing a for loop `for(i
in 1:length(sheets)){read_excel(sheets[i])}`. These are very powerful
functions we will learn more about later. For now, it’s enough to
recognize why we have used it here. You can find more info in
[Chapter 21 of the R4ds book](http://r4ds.had.co.nz/iteration.html).

# Exercise 1: Investigating the North-Atlantic Cod

Now we are ready to dive into our data. First, We seek to replicate the
following figure from the Millenium Ecosystem Assessment Project using
the RAM data.

![](http://espm-157.carlboettiger.info/img/cod.jpg)

**How does your graph compare to the one presented above?**

-----

# Exercise 2: Group Assignment

## Stock Collapses

We seek to replicate the temporal trend in stock declines shown in [Worm
et al 2006](http://doi.org/10.1126/science.1132294):

![](http://espm-157.carlboettiger.info/img/worm2006.jpg)
