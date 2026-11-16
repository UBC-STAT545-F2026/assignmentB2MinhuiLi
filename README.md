
<!-- README.md is generated from README.Rmd. Please edit that file -->

# Package description: assignmentB2MinhuiLi

The `assignmentB2MinhuiLi` package provides a function,
`count_all_missing_by_group()`, that counts missing values for all
columns by group. Given a data frame `data` and a column `group`,
`count_all_missing_by_group()` creates a new data frame with one row per
level of `group`. The first column of the output data frame contains the
levels of `group`, and the rest of the columns contain the number of
missing values for all columns in `data` except `group`. This function
is a wrapper around the `group_by()` and `summarize()` functions in the
`dplyr` package.

## Installation

Package installation can be done directly by calling
`devtools::install_github("UBC-STAT545-F2026/assignmentB2MinhuiLi")`

You can install the development version of assignmentB2MinhuiLi from
[GitHub](https://github.com/) with:

``` r
# install.packages("pak")
pak::pak("UBC-STAT545-F2026/assignmentB2MinhuiLi")
```

## Example

Load the package:

``` r
library(assignmentB2MinhuiLi)
```

This example computes the number of missing values in the `airquality`
dataset grouped by the `Month` column.

``` r
count_all_missing_by_group(airquality, Month)
#> # A tibble: 5 × 6
#>   Month Ozone Solar.R  Wind  Temp   Day
#>   <int> <int>   <int> <int> <int> <int>
#> 1     5     5       4     0     0     0
#> 2     6    21       0     0     0     0
#> 3     7     5       0     0     0     0
#> 4     8     5       3     0     0     0
#> 5     9     1       0     0     0     0
```

This example has the same output as the last example, but shows off an
alternative way of invoking the `count_all_missing_by_group()`: piping
the dataset into the function.

``` r
airquality |> count_all_missing_by_group(Month) 
#> # A tibble: 5 × 6
#>   Month Ozone Solar.R  Wind  Temp   Day
#>   <int> <int>   <int> <int> <int> <int>
#> 1     5     5       4     0     0     0
#> 2     6    21       0     0     0     0
#> 3     7     5       0     0     0     0
#> 4     8     5       3     0     0     0
#> 5     9     1       0     0     0     0
```

The optional `.groups` argument allows us to keep the output grouped by
the grouping column. See example below; notice how the output is a
grouped tibble, rather than the ungrouped tibble output of the earlier
examples.

``` r
count_all_missing_by_group(airquality, Month, .groups = "keep")
#> # A tibble: 5 × 6
#> # Groups:   Month [5]
#>   Month Ozone Solar.R  Wind  Temp   Day
#>   <int> <int>   <int> <int> <int> <int>
#> 1     5     5       4     0     0     0
#> 2     6    21       0     0     0     0
#> 3     7     5       0     0     0     0
#> 4     8     5       3     0     0     0
#> 5     9     1       0     0     0     0
```
