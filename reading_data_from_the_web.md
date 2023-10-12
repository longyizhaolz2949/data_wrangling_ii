reading_data_from_the_web
================
Longyi Zhao
2023-10-12

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.3     ✔ readr     2.1.4
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.0
    ## ✔ ggplot2   3.4.3     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.2     ✔ tidyr     1.3.0
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(rvest)
```

    ## 
    ## Attaching package: 'rvest'
    ## 
    ## The following object is masked from 'package:readr':
    ## 
    ##     guess_encoding

``` r
library(httr)
```

``` r
nsduh_url = "http://samhda.s3-us-gov-west-1.amazonaws.com/s3fs-public/field-uploads/2k15StateFiles/NSDUHsaeShortTermCHG2015.htm"

nsduh_html = read_html(nsduh_url)
```

import every table? first() read the first table remove notes

``` r
marj_use_df = 
  nsduh_html |>
  html_table() |>
  first() |>
  slice(-1)
```

import star wars

``` r
swm_url = "https://www.imdb.com/list/ls070150896/"
  
swm_html = read_html (swm_url)
```

use selectorGadget

``` r
swm_html |>
  html_elements(".lister-item-header a") |>
  html_text()
```

    ## [1] "Star Wars: Episode I - The Phantom Menace"     
    ## [2] "Star Wars: Episode II - Attack of the Clones"  
    ## [3] "Star Wars: Episode III - Revenge of the Sith"  
    ## [4] "Star Wars: Episode IV - A New Hope"            
    ## [5] "Star Wars: Episode V - The Empire Strikes Back"
    ## [6] "Star Wars: Episode VI - Return of the Jedi"    
    ## [7] "Star Wars: Episode VII - The Force Awakens"    
    ## [8] "Star Wars: Episode VIII - The Last Jedi"       
    ## [9] "Star Wars: The Rise Of Skywalker"

``` r
swm_gross_rev_vec = swm_html |>
  html_elements(".text-small:nth-child(7) span:nth-child(5)") |>
  html_text()
```

get water daya from nyc

``` r
nyc_water_df = 
  GET("https://data.cityofnewyork.us/resource/ia2d-e54m.csv") |>
  content("parsed")
```

    ## Rows: 44 Columns: 4
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## dbl (4): year, new_york_city_population, nyc_consumption_million_gallons_per...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

BRFSS data

``` r
brfss_df = 
  GET("https://chronicdata.cdc.gov/resource/acme-vg9e.csv", 
      query = list("$limit" = 5000)) |>
  content()
```

    ## Rows: 5000 Columns: 23
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (16): locationabbr, locationdesc, class, topic, question, response, data...
    ## dbl  (6): year, sample_size, data_value, confidence_limit_low, confidence_li...
    ## lgl  (1): locationid
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
