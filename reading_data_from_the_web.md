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
