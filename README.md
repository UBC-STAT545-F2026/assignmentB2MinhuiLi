
<!-- README.md is generated from README.Rmd. Please edit that file -->

# Package description: assignmentB2MinhuiLi

The `assignmentB2MinhuiLi` package provides
`count_all_missing_by_group()`, a function that counts missing values
for all columns by group. Given a data frame `data` and a column
`group`, `count_all_missing_by_group()` creates a new data frame with
one row per level of `group`. The first column of the output data frame
contains the levels of `group`, and the rest of the columns contain the
number of missing values for all columns in `data` except `group`. This
function is a wrapper around the `group_by()` and `summarize()`
functions in the `dplyr` package.

## Installation

Package installation can be done directly by calling:

``` r
devtools::install_github("UBC-STAT545-F2026/assignmentB2MinhuiLi")
#> Warning: `install_github()` was deprecated in devtools 2.5.0.
#> ℹ Please use pak::pak("user/repo") instead.
#> This warning is displayed once per session.
#> Call `lifecycle::last_lifecycle_warnings()` to see where this warning was
#> generated.
#> Using GitHub PAT from the git credential store.
#> Downloading GitHub repo UBC-STAT545-F2026/assignmentB2MinhuiLi@HEAD
#> 
#> ── R CMD build ─────────────────────────────────────────────────────────────────
#>       ✔  checking for file 'C:\Users\11637\AppData\Local\Temp\RtmpioYRP5\remotes4f4c1b254246\UBC-STAT545-F2026-assignmentB2MinhuiLi-bb65753/DESCRIPTION'
#>       ─  preparing 'assignmentB2MinhuiLi':
#>    checking DESCRIPTION meta-information ...  ✔  checking DESCRIPTION meta-information
#>       ─  checking for LF line-endings in source and make files and shell scripts
#>   ─  checking for empty or unneeded directories
#>      NB: this package now depends on R (>=        NB: this package now depends on R (>= 4.1.0)
#>      WARNING: Added dependency on R >= 4.1.0 because package code uses the
#>      pipe |> or function shorthand \(...) syntax added in R 4.1.0.
#>      File(s) using such syntax:
#>        'count_all_missing_by_group.Rd' 'count_missing_values.R'
#>   ─  building 'assignmentB2MinhuiLi_0.1.0.tar.gz'
#>      
#> 
library(assignmentB2MinhuiLi)
```

## Usage/Example

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
