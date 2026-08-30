# Yahoo Finance Live Prices

This function will use the json api to retrieve live prices from Yahoo
finance.

## Usage

``` r
yf_live_prices(ticker)
```

## Arguments

- ticker:

  a single ticker symbol

## Value

a tibble with live prices

## Examples

``` r
yfR::yf_live_prices("PETR4.SA")
#> # A tibble: 1 × 5
#>   ticker   time_stamp          price last_price daily_change
#>   <chr>    <dttm>              <dbl>      <dbl>        <dbl>
#> 1 PETR4.SA 2026-08-28 20:05:38  43.6       42.7       0.0199
```
