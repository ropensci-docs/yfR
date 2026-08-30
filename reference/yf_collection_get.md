# Downloads a collection of data from Yahoo Finance

This function will use a set collection of YF data, such as index
components and will download all data from Yahoo Finance using
[`yf_get`](https://docs.ropensci.org/yfR/reference/yf_get.md).

## Usage

``` r
yf_collection_get(
  collection,
  first_date = Sys.Date() - 30,
  last_date = Sys.Date(),
  do_parallel = FALSE,
  do_cache = TRUE,
  cache_folder = yf_cachefolder_get(),
  ...
)
```

## Arguments

- collection:

  A collection to fetch data (e.g. "SP500", "IBOV", "FTSE" ). See
  function
  [`yf_get_available_collections`](https://docs.ropensci.org/yfR/reference/yf_get_available_collections.md)
  for finding all available collections

- first_date:

  The first date of query (Date or character as YYYY-MM-DD)

- last_date:

  The last date of query (Date or character as YYYY-MM-DD)

- do_parallel:

  Flag for using parallel or not (default = FALSE). Before using
  parallel, make sure you call function future::plan() first. See
  \<https://furrr.futureverse.org/\> for more details.

- do_cache:

  Use cache system? (default = TRUE)

- cache_folder:

  Where to save cache files? (default = yfR::yf_cachefolder_get() )

- ...:

  Other arguments passed to
  [`yf_get`](https://docs.ropensci.org/yfR/reference/yf_get.md)

## Value

A data frame with financial prices from collection

## Examples

``` r

# \donttest{
df_yf <- yf_collection_get(collection = "IBOV",
                           first_date = Sys.Date() - 30,
                           last_date = Sys.Date()
)
#> 
#> ── Fetching price collection for IBOV ──────────────────────────────────────────
#> ✔ Got IBOV composition with 88 rows
#> 
#> ── Running yfR for 88 stocks | 2026-07-31 --> 2026-08-30 (30 days) ──
#> 
#> ℹ Downloading data for benchmark ticker ^BVSP
#> ℹ (1/88) Fetching data for ABEV3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Good stuff!
#> ℹ (2/88) Fetching data for ALPA4.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Got it!
#> ℹ (3/88) Fetching data for AMER3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Looking good!
#> ℹ (4/88) Fetching data for ASAI3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Got it!
#> ℹ (5/88) Fetching data for AXIA3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Boa!
#> ℹ (6/88) Fetching data for AXIA7.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Mas bah tche, que coisa linda!
#> ℹ (7/88) Fetching data for AZUL4.SA
#> !   - not cached
#> ✖   - error in download..
#> ℹ (8/88) Fetching data for B3SA3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Good job !
#> ℹ (9/88) Fetching data for BBAS3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- All OK!
#> ℹ (10/88) Fetching data for BBDC3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Well done !
#> ℹ (11/88) Fetching data for BBDC4.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Mas bah tche, que coisa linda!
#> ℹ (12/88) Fetching data for BBSE3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Got it!
#> ℹ (13/88) Fetching data for BEEF3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- You got it !
#> ℹ (14/88) Fetching data for BIDI11.SA
#> !   - not cached
#> ✖   - error in download..
#> ℹ (15/88) Fetching data for BPAC11.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Good stuff!
#> ℹ (16/88) Fetching data for BPAN4.SA
#> !   - not cached
#> ✖   - error in download..
#> ℹ (17/88) Fetching data for BRAP4.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Nice!
#> ℹ (18/88) Fetching data for BRFS3.SA
#> !   - not cached
#> ✖   - error in download..
#> ℹ (19/88) Fetching data for BRKM5.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- You got it !
#> ℹ (20/88) Fetching data for BRML3.SA
#> !   - not cached
#> ✖   - error in download..
#> ℹ (21/88) Fetching data for CASH3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Good job !
#> ℹ (22/88) Fetching data for CCRO3.SA
#> !   - not cached
#> ✖   - error in download..
#> ℹ (23/88) Fetching data for CIEL3.SA
#> !   - not cached
#> ✖   - error in download..
#> ℹ (24/88) Fetching data for CMIG4.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Time for some tea?
#> ℹ (25/88) Fetching data for COGN3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Time for some tea?
#> ℹ (26/88) Fetching data for CPFE3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Good stuff!
#> ℹ (27/88) Fetching data for CPLE6.SA
#> !   - not cached
#> ✖   - error in download..
#> ℹ (28/88) Fetching data for CRFB3.SA
#> !   - not cached
#> ✖   - error in download..
#> ℹ (29/88) Fetching data for CSAN3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Got it!
#> ℹ (30/88) Fetching data for CSNA3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Time for some tea?
#> ℹ (31/88) Fetching data for CVCB3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Got it!
#> ℹ (32/88) Fetching data for CYRE3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Good stuff!
#> ℹ (33/88) Fetching data for DXCO3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Good stuff!
#> ℹ (34/88) Fetching data for ECOR3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Nice!
#> ℹ (35/88) Fetching data for EGIE3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- All OK!
#> ℹ (36/88) Fetching data for EMBJ3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Nice!
#> ℹ (37/88) Fetching data for ENBR3.SA
#> !   - not cached
#> ✖   - error in download..
#> ℹ (38/88) Fetching data for ENEV3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Youre doing good!
#> ℹ (39/88) Fetching data for ENGI11.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Got it!
#> ℹ (40/88) Fetching data for EQTL3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Nice!
#> ℹ (41/88) Fetching data for EZTC3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Nice!
#> ℹ (42/88) Fetching data for FLRY3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Good stuff!
#> ℹ (43/88) Fetching data for GGBR4.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- You got it !
#> ℹ (44/88) Fetching data for GOAU4.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Looking good!
#> ℹ (45/88) Fetching data for GOLL4.SA
#> !   - not cached
#> ✖   - error in download..
#> ℹ (46/88) Fetching data for HAPV3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Got it!
#> ℹ (47/88) Fetching data for HYPE3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Good job !
#> ℹ (48/88) Fetching data for IGTI11.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Time for some tea?
#> ℹ (49/88) Fetching data for IRBR3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Got it!
#> ℹ (50/88) Fetching data for ITSA4.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Youre doing good!
#> ℹ (51/88) Fetching data for ITUB4.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- You got it !
#> ℹ (52/88) Fetching data for JBSS3.SA
#> !   - not cached
#> ✖   - error in download..
#> ℹ (53/88) Fetching data for JHSF3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Time for some tea?
#> ℹ (54/88) Fetching data for KLBN11.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Youre doing good!
#> ℹ (55/88) Fetching data for LCAM3.SA
#> !   - not cached
#> ✖   - error in download..
#> ℹ (56/88) Fetching data for LREN3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Time for some tea?
#> ℹ (57/88) Fetching data for LWSA3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Nice!
#> ℹ (58/88) Fetching data for MGLU3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Good job !
#> ℹ (59/88) Fetching data for MRFG3.SA
#> !   - not cached
#> ✖   - error in download..
#> ℹ (60/88) Fetching data for MRVE3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Time for some tea?
#> ℹ (61/88) Fetching data for MULT3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Looking good!
#> ℹ (62/88) Fetching data for NTCO3.SA
#> !   - not cached
#> ✖   - error in download..
#> ℹ (63/88) Fetching data for PCAR3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Time for some tea?
#> ℹ (64/88) Fetching data for PETR3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Good stuff!
#> ℹ (65/88) Fetching data for PETR4.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- All OK!
#> ℹ (66/88) Fetching data for PETZ3.SA
#> !   - not cached
#> ✖   - error in download..
#> ℹ (67/88) Fetching data for PRIO3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Youre doing good!
#> ℹ (68/88) Fetching data for QUAL3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Nice!
#> ℹ (69/88) Fetching data for RADL3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- All OK!
#> ℹ (70/88) Fetching data for RAIL3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Looking good!
#> ℹ (71/88) Fetching data for RDOR3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Good stuff!
#> ℹ (72/88) Fetching data for RENT3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Good stuff!
#> ℹ (73/88) Fetching data for SANB11.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Good job !
#> ℹ (74/88) Fetching data for SBSP3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Well done !
#> ℹ (75/88) Fetching data for SOMA3.SA
#> !   - not cached
#> ✖   - error in download..
#> ℹ (76/88) Fetching data for SULA11.SA
#> !   - not cached
#> ✖   - error in download..
#> ℹ (77/88) Fetching data for SUZB3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Got it!
#> ℹ (78/88) Fetching data for TAEE11.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Looking good!
#> ℹ (79/88) Fetching data for TIMS3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Got it!
#> ℹ (80/88) Fetching data for TOTS3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Time for some tea?
#> ℹ (81/88) Fetching data for UGPA3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Well done !
#> ℹ (82/88) Fetching data for USIM5.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Well done !
#> ℹ (83/88) Fetching data for VALE3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Good stuff!
#> ℹ (84/88) Fetching data for VBBR3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Youre doing good!
#> ℹ (85/88) Fetching data for VIIA3.SA
#> !   - not cached
#> ✖   - error in download..
#> ℹ (86/88) Fetching data for VIVT3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Good stuff!
#> ℹ (87/88) Fetching data for WEGE3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Time for some tea?
#> ℹ (88/88) Fetching data for YDUQ3.SA
#> !   - not cached
#> ✔   - cache saved successfully
#> ✔   - got 20 valid rows (2026-07-31 --> 2026-08-27)
#> ✔   - got 95% of valid prices -- Good job !
#> ℹ Binding price data
#> 
#> ── Diagnostics ─────────────────────────────────────────────────────────────────
#> ✔ Returned dataframe with 1380 rows -- Mais faceiro que guri de bombacha nova!
#> ℹ Using 222.3 kB at /tmp/Rtmpl7WiWC/yf_cache for 71 cache files
#> ℹ Out of 88 requested tickers, you got 69 (78%)
# }
```
