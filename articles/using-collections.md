# Using Collections

## Fetching collections of prices

Collections are just a bundle of tickers pre-organized in the package.
For example, collection `SP500` represents the current composition of
the SP500 index.

The available collections are:

``` r

available_collections <- yfR::yf_get_available_collections(
  print_description = TRUE
  )
```

    ## 

    ## ── Description of Available Collections ──

    ## 

    ## ℹ SP500: The SP500 index (US MARKET) - Ticker = ^GSPC

    ## ℹ IBOV: The Ibovespa index (BR MARKET) - Ticker = ^BVSP

    ## ℹ FTSE: The FTSE index (UK MARKET) - Ticker = ^FTSE

    ## ℹ DOW: The DOW index (US MARKET) - Ticker = ^DJI

    ## ℹ testthat-collection: A (small) testing index for testthat() -- dev stuff, dont use it!

``` r

available_collections
```

    ## [1] "SP500"               "IBOV"                "FTSE"               
    ## [4] "DOW"                 "testthat-collection"

One can download the composition of the collection with
`yf_collection_get`:

``` r

library(yfR)

# be patient, it takes a while
df_yf <- yf_collection_get("SP500")

head(df_yf)
```
