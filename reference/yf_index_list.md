# Get available indices in package

This function will return all available market indices that are
registered in the package.

## Usage

``` r
yf_index_list(print_description = FALSE)
```

## Arguments

- print_description:

  Logical (TRUE/FALSE) - flag for printing description of available
  indices/collections

## Value

A vector of mkt indices

## Examples

``` r

indices <- yf_index_list()
indices
#> [1] "SP500"               "IBOV"                "FTSE"               
#> [4] "DOW"                 "testthat-collection"
```
