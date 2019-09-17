20190917\_Data\_Wrangling\_Practice
================
Kevin S.W.
9/17/2019

## Load in a dataset

``` r
# Reads in a dataset
# 2 types of paths; absolute (the full path) vs relative (only refers to the relevant files)
# getwd() pulls the absolute path until your current working directory

# instead uses a relative path. the "." means "start here"; ".." means "one directory up"; "..." means 2 up...
litters_data <- read_csv(file = "./data/FAS_litters.csv")   # uses relative path
```

    ## Parsed with column specification:
    ## cols(
    ##   Group = col_character(),
    ##   `Litter Number` = col_character(),
    ##   `GD0 weight` = col_double(),
    ##   `GD18 weight` = col_double(),
    ##   `GD of Birth` = col_double(),
    ##   `Pups born alive` = col_double(),
    ##   `Pups dead @ birth` = col_double(),
    ##   `Pups survive` = col_double()
    ## )

``` r
litters_data <- janitor::clean_names(litters_data)          # the "::" means x package::function in package
```
