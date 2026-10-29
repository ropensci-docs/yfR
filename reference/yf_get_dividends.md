# Get Yahoo Finance Dividends from a single stock

This function will use the json api to retrieve dividends from Yahoo
finance.

## Usage

``` r
yf_get_dividends(ticker, first_date = Sys.Date() - 365, last_date = Sys.Date())
```

## Arguments

- ticker:

  a single ticker symbol

- first_date:

  The first date of query (Date or character as YYYY-MM-DD)

- last_date:

  The last date of query (Date or character as YYYY-MM-DD)

## Value

a tibble with dividends

## Examples

``` r
yf_get_dividends(ticker = "PETR4.SA")
#> ℹ Be aware that YF does not provide a consistent dividend database. Use this function with caution.
#> # A tibble: 4 × 3
#>   ref_date   ticker   dividend
#>   <date>     <chr>       <dbl>
#> 1 2025-12-23 PETR4.SA    0.952
#> 2 2026-04-23 PETR4.SA    0.663
#> 3 2026-06-02 PETR4.SA    0.701
#> 4 2026-08-24 PETR4.SA    1.35 
```
