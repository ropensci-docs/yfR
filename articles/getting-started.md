# Getting Started

## Examples

Here you’ll find a series of example of calls to
[`yf_get()`](https://docs.ropensci.org/yfR/reference/yf_get.md). Most
arguments are self-explanatory, but you can find more details at the
help files.

The steps of the algorithm are:

1.  check cache files for existing data
2.  if not in cache, fetch stock prices from YF and clean up the raw
    data
3.  write cache file if not available
4.  calculate all returns
5.  build diagnostics
6.  return the data to the user

### Fetching a single stock price

``` r

library(yfR)

# set options for algorithm
my_ticker <- 'GM'
first_date <- Sys.Date() - 30
last_date <- Sys.Date()

# fetch data
df_yf <- yf_get(tickers = my_ticker, 
                first_date = first_date,
                last_date = last_date)

# output is a tibble with data
head(df_yf)
```

    ## # A tibble: 6 × 11
    ##   ticker ref_date   price_open price_high price_low price_close  volume
    ##   <chr>  <date>          <dbl>      <dbl>     <dbl>       <dbl>   <dbl>
    ## 1 GM     2026-09-29       80.8       81.1      79.6        80.5 6250800
    ## 2 GM     2026-09-30       80.7       80.8      76.9        77   9765600
    ## 3 GM     2026-10-01       76.5       79.4      76.4        79.3 8437600
    ## 4 GM     2026-10-02       79.9       79.9      78.0        78.3 9088600
    ## 5 GM     2026-10-05       79.0       81.0      78.7        80.2 6490600
    ## 6 GM     2026-10-06       81.4       82.2      80.7        82.0 5209600
    ## # ℹ 4 more variables: price_adjusted <dbl>, ret_adjusted_prices <dbl>,
    ## #   ret_closing_prices <dbl>, cumret_adjusted_prices <dbl>

### Fetching many stock prices

``` r

library(yfR)
library(ggplot2)

my_ticker <- c('TSLA', 'GM', 'MMM')
first_date <- Sys.Date() - 100
last_date <- Sys.Date()

df_yf_multiple <- yf_get(tickers = my_ticker, 
                         first_date = first_date,
                         last_date = last_date)


p <- ggplot(df_yf_multiple, aes(x = ref_date, y = price_adjusted,
                                color = ticker)) + 
  geom_line()

p
```

![](getting-started_files/figure-html/unnamed-chunk-3-1.png)

### Fetching daily/weekly/monthly/yearly price data

``` r

library(yfR)
library(ggplot2)
library(dplyr)

my_ticker <- 'GE'
first_date <- '2005-01-01'
last_date <- Sys.Date()

df_dailly <- yf_get(tickers = my_ticker, 
                    first_date, last_date, 
                    freq_data = 'daily') %>%
  mutate(freq = 'daily')

df_weekly <- yf_get(tickers = my_ticker, 
                    first_date, last_date, 
                    freq_data = 'weekly') %>%
  mutate(freq = 'weekly')

df_monthly <- yf_get(tickers = my_ticker, 
                     first_date, last_date, 
                     freq_data = 'monthly') %>%
  mutate(freq = 'monthly')

df_yearly <- yf_get(tickers = my_ticker, 
                    first_date, last_date, 
                    freq_data = 'yearly') %>%
  mutate(freq = 'yearly')

# bind it all together for plotting
df_allfreq <- bind_rows(
  list(df_dailly, df_weekly, df_monthly, df_yearly)
) %>%
  mutate(freq = factor(freq, 
                       levels = c('daily', 
                                  'weekly',
                                  'monthly',
                                  'yearly'))) # make sure the order in plot is right

p <- ggplot(df_allfreq, aes(x = ref_date, y = price_adjusted)) + 
  geom_line() + 
  facet_grid(freq ~ ticker) + 
  theme_minimal() + 
  labs(x = '', y = 'Adjusted Prices')

print(p)
```

![](getting-started_files/figure-html/unnamed-chunk-4-1.png)

### Changing format to wide

``` r

library(yfR)
library(ggplot2)

my_ticker <- c('TSLA', 'GM', 'MMM')
first_date <- Sys.Date() - 100
last_date <- Sys.Date()

df_yf_multiple <- yf_get(tickers = my_ticker, 
                         first_date = first_date,
                         last_date = last_date)

print(df_yf_multiple)
```

    ## # A tibble: 213 × 11
    ##    ticker ref_date   price_open price_high price_low price_close   volume
    ##  * <chr>  <date>          <dbl>      <dbl>     <dbl>       <dbl>    <dbl>
    ##  1 GM     2026-07-21       76.1       80.1      74.8        79.5 11919800
    ##  2 GM     2026-07-22       80.5       84.3      80.0        82.1 13059500
    ##  3 GM     2026-07-23       81.4       81.7      79          80.7  9512900
    ##  4 GM     2026-07-24       80.5       83.8      80.4        82.6  5605600
    ##  5 GM     2026-07-27       85         87.1      84.1        87.0  9870000
    ##  6 GM     2026-07-28       87.6       91.2      87.2        90.3 13382300
    ##  7 GM     2026-07-29       90.7       91.8      89.1        89.4  7981500
    ##  8 GM     2026-07-30       89.7       89.8      86.6        88.4  6229000
    ##  9 GM     2026-07-31       88.8       89.1      87.0        88.9  6678000
    ## 10 GM     2026-08-03       89.5       90.3      87.3        87.7  4813400
    ## # ℹ 203 more rows
    ## # ℹ 4 more variables: price_adjusted <dbl>, ret_adjusted_prices <dbl>,
    ## #   ret_closing_prices <dbl>, cumret_adjusted_prices <dbl>

``` r

l_wide <- yf_convert_to_wide(df_yf_multiple)

names(l_wide)
```

    ## [1] "price_open"             "price_high"             "price_low"             
    ## [4] "price_close"            "volume"                 "price_adjusted"        
    ## [7] "ret_adjusted_prices"    "ret_closing_prices"     "cumret_adjusted_prices"

``` r

prices_wide <- l_wide$price_adjusted
head(prices_wide)
```

    ## # A tibble: 6 × 4
    ##   ref_date      GM   MMM  TSLA
    ##   <date>     <dbl> <dbl> <dbl>
    ## 1 2026-07-21  79.4  170.  379.
    ## 2 2026-07-22  82.0  170.  374.
    ## 3 2026-07-23  80.5  169.  320.
    ## 4 2026-07-24  82.5  172.  313.
    ## 5 2026-07-27  86.9  177.  309.
    ## 6 2026-07-28  90.1  182.  307.
