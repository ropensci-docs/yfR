# Get current composition of stock indices

Get current composition of stock indices

## Usage

``` r
yf_index_composition(
  mkt_index,
  do_cache = TRUE,
  cache_folder = yf_cachefolder_get(),
  force_fallback = FALSE
)
```

## Arguments

- mkt_index:

  the index (e.g. IBOV, SP500, FTSE)

- do_cache:

  Use cache system? (default = TRUE)

- cache_folder:

  Where to save cache files? (default = yfR::yf_cachefolder_get() )

- force_fallback:

  Logical (TRUE/FALSE). Forces the function to use the fallback system

## Value

A dataframe with the index composition (column might vary)

## Examples

``` r
df_sp500 <- yf_index_composition("SP500")
#> ✔ Got SP500 composition with 503 rows
```
