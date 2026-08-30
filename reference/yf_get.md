# Download financial data from Yahoo Finance

Based on a ticker (id of a stock) and time period, this function will
download stock price data from Yahoo Finance and organizes it in the
long format. Yahoo Finance \<https://finance.yahoo.com/\> provides a
vast repository of stock price data around the globe. It cover a
significant number of markets and assets, being used extensively in
academic research and teaching. In the website you can lookup the ticker
of a company.

## Usage

``` r
yf_get(
  tickers,
  first_date = Sys.Date() - 30,
  last_date = Sys.Date(),
  thresh_bad_data = 0.75,
  bench_ticker = "^GSPC",
  type_return = "arit",
  freq_data = "daily",
  how_to_aggregate = "last",
  do_complete_data = FALSE,
  do_cache = TRUE,
  cache_folder = yf_cachefolder_get(),
  do_parallel = FALSE,
  be_quiet = FALSE
)
```

## Arguments

- tickers:

  A single or vector of tickers. If not sure whether the ticker is
  available, search for it in YF \<https://finance.yahoo.com/\>.

- first_date:

  The first date of query (Date or character as YYYY-MM-DD)

- last_date:

  The last date of query (Date or character as YYYY-MM-DD)

- thresh_bad_data:

  A percentage threshold for defining bad data. The dates of the
  benchmark ticker are compared to each asset. If the percentage of
  non-missing dates with respect to the benchmark ticker is lower than
  thresh_bad_data, the function will ignore the asset (default = 0.75)

- bench_ticker:

  The ticker of the benchmark asset used to compare dates. My suggestion
  is to use the main stock index of the market from where the data is
  coming from (default = ^GSPC (SP500, US market))

- type_return:

  Type of price return to calculate: 'arit' - arithmetic (default),
  'log' - log returns.

- freq_data:

  Frequency of financial data: 'daily' (default), 'weekly', 'monthly',
  'yearly'

- how_to_aggregate:

  Defines whether to aggregate the data using the first observations of
  the aggregating period or last ('first', 'last'). For example, if
  freq_data = 'yearly' and how_to_aggregate = 'last', the last available
  day of the year will be used for all aggregated values such as
  price_adjusted. (Default = "last")

- do_complete_data:

  Return a complete/balanced dataset? If TRUE, all missing pairs of
  ticker-date will be replaced by NA or closest price (see input
  do_fill_missing_prices). Default = FALSE.

- do_cache:

  Use cache system? (default = TRUE)

- cache_folder:

  Where to save cache files? (default = yfR::yf_cachefolder_get() )

- do_parallel:

  Flag for using parallel or not (default = FALSE). Before using
  parallel, make sure you call function future::plan() first. See
  \<https://furrr.futureverse.org/\> for more details.

- be_quiet:

  Flag for not printing statements (default = FALSE)

## Value

A dataframe with the financial data for working days, when markets are
open. All price data is **measured** at the unit of the financial
exchange. For example, price data for META (NYSE/US) is measures in
dollars, while price data for PETR3.SA (B3/BR) is measured in Reais
(Brazilian currency).

The return dataframe contains the following columns:

- ticker:

  The requested tickers (ids of stocks)

- ref_date:

  The reference day (this can also be year/month/week when using
  argument freq_data)

- price_open:

  The opening price of the day/period

- price_high:

  The highest price of the day/period

- price_close:

  The close/last price of the day/period

- volume:

  The financial volume of the day/period

- price_adjusted:

  The stock price adjusted for corporate events such as splits,
  dividends and others – this is usually what you want/need for studying
  stocks as it represents the actual financial performance of
  stockholders

- ret_adjusted_prices:

  The arithmetic or log return (see input type_return) for the adjusted
  stock prices

- ret_adjusted_prices:

  The arithmetic or log return (see input type_return) for the closing
  stock prices

- cumret_adjusted_prices:

  The accumulated arithmetic/log return for the period (starts at 100%)

## The cache system

The yfR\`s cache system is basically a bunch of rds files that are saved
every time data is imported from YF. It indexes all data by ticker and
time period. Whenever a user asks for a dataset, it first checks if the
ticker/time period exists in cache and, if it does, loads the data from
the rds file.

By default, a temporary folder is used (see function
[yf_cachefolder_get](https://docs.ropensci.org/yfR/reference/yf_cachefolder_get.md),
which means that all cache files are session-persistent. In practice,
whenever you restart your R/RStudio session, all cache files are lost.
This is a choice I've made due to the fact that merging adjusted stock
price data after corporate events (dividends/splits) is a mess and prone
to errors. This only happens for stock price data, and not indices data.

If you really need a persistent cache folder, which is Ok for indices
data, simply set a path with argument cache_folder (see warning
section).

## Warning

Be aware that when using cache system in a local folder (and not the
default tempdir()), the aggregate prices series might not match if a
split or dividends event happens in between cache files.

## Examples

``` r

# \donttest{
tickers <- c("TSLA", "MMM")

first_date <- Sys.Date() - 30
last_date <- Sys.Date()

df_yf <- yf_get(
  tickers = tickers,
  first_date = first_date,
  last_date = last_date
)
#> 
#> ── Running yfR for 2 stocks | 2026-07-31 --> 2026-08-30 (30 days) ──
#> 
#> ℹ Downloading data for benchmark ticker ^GSPC
#> ℹ (1/2) Fetching data for MMM
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 21 valid rows (2026-07-31 --> 2026-08-28)
#> ✔   - got 100% of valid prices -- Got it!
#> ℹ (2/2) Fetching data for TSLA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 21 valid rows (2026-07-31 --> 2026-08-28)
#> ✔   - got 100% of valid prices -- Well done !
#> ℹ Binding price data
#> 
#> ── Diagnostics ─────────────────────────────────────────────────────────────────
#> ✔ Returned dataframe with 42 rows -- Well done !
#> ℹ Using 231.4 kB at /tmp/Rtmpl7WiWC/yf_cache for 74 cache files
#> ℹ Out of 2 requested tickers, you got 2 (100%)

print(df_yf)
#> # A tibble: 42 × 11
#>    ticker ref_date   price_open price_high price_low price_close  volume
#>  * <chr>  <date>          <dbl>      <dbl>     <dbl>       <dbl>   <dbl>
#>  1 MMM    2026-07-31       176.       177.      175.        176. 2676800
#>  2 MMM    2026-08-03       178        179.      176.        177. 2749500
#>  3 MMM    2026-08-04       179.       182.      177.        181. 2980000
#>  4 MMM    2026-08-05       181.       183.      181.        182. 2728600
#>  5 MMM    2026-08-06       182.       184.      179.        181. 2547000
#>  6 MMM    2026-08-07       180.       184.      179.        183. 2430400
#>  7 MMM    2026-08-10       183.       184.      181.        182. 1942500
#>  8 MMM    2026-08-11       182.       184.      182.        183. 2335500
#>  9 MMM    2026-08-12       184.       184.      181.        184. 2647500
#> 10 MMM    2026-08-13       184.       185.      180.        183. 2852800
#> # ℹ 32 more rows
#> # ℹ 4 more variables: price_adjusted <dbl>, ret_adjusted_prices <dbl>,
#> #   ret_closing_prices <dbl>, cumret_adjusted_prices <dbl>
# }
```
