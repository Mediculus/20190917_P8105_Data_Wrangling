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
# the "::" means package::function in package. Typically; if you only need 1 fx from a package, use the "::"
litters_data <- janitor::clean_names(litters_data)

#skimr::skim also "skims" the data
```

other arguments in read\_\* also has col\_names. Default is TRUE. if
FALSE, it will name it x1, x2…

``` r
# Practice loading FAS_pups.csv
pups_data <- read_csv(file = "./data/FAS_pups.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   `Litter Number` = col_character(),
    ##   Sex = col_double(),
    ##   `PD ears` = col_double(),
    ##   `PD eyes` = col_double(),
    ##   `PD pivot` = col_double(),
    ##   `PD walk` = col_double()
    ## )

``` r
pups_data <- janitor::clean_names(pups_data)
```

``` r
# Reads in a dataset
# 2 types of paths; absolute (the full path) vs relative (only refers to the relevant files)
# getwd() pulls the absolute path until your current working directory

# instead uses a relative path. the "." means "start here"; ".." means "one directory up"; "..." means 2 up...
litters_data2 <- read_csv(file = "./data/FAS_litters.csv",
                         skip = 10, col_names = FALSE)   # uses relative path
```

    ## Parsed with column specification:
    ## cols(
    ##   X1 = col_character(),
    ##   X2 = col_character(),
    ##   X3 = col_double(),
    ##   X4 = col_double(),
    ##   X5 = col_double(),
    ##   X6 = col_double(),
    ##   X7 = col_double(),
    ##   X8 = col_double()
    ## )

``` r
# the "::" means package::function in package. Typically; if you only need 1 fx from a package, use the "::"
litters_data2 <- janitor::clean_names(litters_data2)
```

During data import, R will try to automatically parse data and “guess”
what category a column is (logic/double/etc)

by having col\_types inside read\_\*, we can assign the types of data
ourselves. example:

``` r
litters_data3 <- read_csv(file = "./data/FAS_litters.csv",
                         col_types = cols(
                          `Group` = col_character(),
                          `Litter Number` = col_character(),  # `content` includes the space
                          `GD0 weight` = col_double(),
                          `GD18 weight` = col_double(),
                          `GD of Birth` = col_integer(),
                          `Pups born alive` = col_integer(),
                          `Pups dead @ birth` = col_integer(),
                         `Pups survive` = col_integer()
                         )
)

# the "::" means package::function in package. Typically; if you only need 1 fx from a package, use the "::"
litters_data3 <- janitor::clean_names(litters_data3)
```

# Read in excel file…

``` r
mlb11_data <- readxl::read_xlsx(path = "./data/mlb11.xlsx", 
                                range = "A1:D7"   # reads only the specified xls cells
                                )

write_csv(mlb11_data, path = "./data/mlb_subset.csv")
```

## Read in SAS…

``` r
pulse_data <- haven::read_sas("./data/public_pulse_data.sas7bdat")
```

The reason why we use read “*" instead of "." is because using "." will
make R "read it as a whole datapoint". With * , it defaults it as a
tibble while . defaults to dataframe. This makes R print out everything
in the data if we use . while we only have a”preview" with \_ .
Furthermore, since R’s base dataframe
