# Returns available collections

Returns available collections

## Usage

``` r
yf_get_available_collections(print_description = FALSE)
```

## Arguments

- print_description:

  Logical (TRUE/FALSE) - flag for printing description of available
  indices/collections

## Value

A string vector with available collections

## Examples

``` r

print(yf_get_available_collections())
#> [1] "SP500"               "IBOV"                "FTSE"               
#> [4] "DOW"                 "testthat-collection"
```
