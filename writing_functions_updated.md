Writing Functions Updated
================

Load key packages.

``` r
library(tidyverse)
library(readxl)
library(rvest)
```

    ## 
    ## Attaching package: 'rvest'

    ## The following object is masked from 'package:readr':
    ## 
    ##     guess_encoding

## Start small!

Everyone loves z scores.

``` r
x_vec = rnorm(20, mean = 10, sd = 3.5)

(x_vec - mean(x_vec)) / sd(x_vec)
```

    ##  [1] -1.044623623 -0.314558700  0.527968106  0.322442123  0.305443829
    ##  [6]  0.825345857  0.931680623 -1.276337004  2.486368474  0.897869186
    ## [11]  0.723259770 -0.005252689 -1.121939310  0.374909623 -1.549717252
    ## [16]  0.753470747 -0.661829867 -1.116589065 -0.404086421 -0.653824407

Write a function to compute z scores.

``` r
z_scores = function(x) {
  
  if (!is.numeric(x)) {
    stop("The input x should be numeric")
  }
  
  if (length(x) < 5) {
    stop("Only compute z scores when the input has 5 or more numbers")
  }
  
  z = (x - mean(x)) / sd(x)
  
  z
  
}
```

Let’s try our function …

``` r
z_scores(x = x_vec)
```

    ##  [1] -1.044623623 -0.314558700  0.527968106  0.322442123  0.305443829
    ##  [6]  0.825345857  0.931680623 -1.276337004  2.486368474  0.897869186
    ## [11]  0.723259770 -0.005252689 -1.121939310  0.374909623 -1.549717252
    ## [16]  0.753470747 -0.661829867 -1.116589065 -0.404086421 -0.653824407

``` r
num_vec = rnorm(123, mean = 14, sd = 0.4)

z_scores(x = num_vec)
```

    ##   [1] -0.18137056 -1.21590672  0.01320758  1.02647383 -1.45781353 -0.07203344
    ##   [7] -1.26233958  0.12911517 -1.66727407 -0.42690134  1.53398082  1.40972830
    ##  [13]  0.52366055 -0.69575723  1.10583903  0.08893665 -0.10170849  1.86094913
    ##  [19]  0.42534653 -0.02752092 -0.58263037 -1.31322801  0.65462150 -0.90980977
    ##  [25]  0.99624019 -1.01141149 -0.54845552 -0.22591992  1.89692437 -0.61715261
    ##  [31]  0.07376667  1.37963640 -2.00767502  0.70121983  0.58542646  2.06397687
    ##  [37] -0.53609454 -0.36420851  1.01443931 -0.28872195 -0.60627631 -0.85472168
    ##  [43]  0.40578195 -0.59149030 -1.12303087  0.69512392  1.91899546 -0.29884354
    ##  [49]  0.08208632 -0.33029228 -1.76933834 -0.15796611  0.60847988  0.48154850
    ##  [55] -1.46850452  0.43480703 -2.80181337  0.49981078  0.10772043 -1.43481496
    ##  [61] -0.77143121 -0.42479183  0.99686780 -0.14905072  0.19724106  0.22188136
    ##  [67]  1.81436121 -2.07334952 -0.17497649  1.00332718  0.49350895  0.07169084
    ##  [73] -0.95085119 -0.45578448 -0.52138759  0.56043359  0.20546509  0.31959386
    ##  [79]  1.91445682  0.66314317 -1.36963462 -0.38976974 -0.74418046 -0.38805751
    ##  [85]  0.07511414  1.94717775 -0.16293626  0.88768855  0.32311386  2.01055466
    ##  [91]  0.16580253  0.41947428 -0.61682559 -0.14955220 -1.12634108 -2.23570104
    ##  [97]  0.70002934 -1.34959732 -1.02198869 -0.01821928 -0.11836584 -1.21859626
    ## [103]  1.29412647  0.40758036  0.31654523 -0.80753515  1.19862851  1.18037307
    ## [109]  1.24963899  0.37320562  2.01907191 -0.32078844 -0.13750001 -1.69470643
    ## [115] -0.49817893 -0.16690287  0.03240182  0.05412246  0.03404631  0.31803032
    ## [121]  1.49647311 -0.21624282 -0.45874427

Let’s break our function …

``` r
z_scores(3)
```

    ## Error in z_scores(3): Only compute z scores when the input has 5 or more numbers

``` r
z_scores("my name is jeff")
```

    ## Error in z_scores("my name is jeff"): The input x should be numeric

## Let’s compute some stuff

Let’s compute and return the mean and sd of a numeric vector.

I’ve written that function and saved it to `source/mean_and_sd.R`, along
with some documentation. For completeness, I’m printing that R script
below.

    ## #' mean_and_sd
    ## #' 
    ## #' Takes a numeric input vector and computes the mean and standard deviation
    ## #'
    ## #' @param x the input vector (must be numeric with 5 or more elements)
    ## #'
    ## #' @returns a dataframe containing the mean and sd of x
    ## #' 
    ## mean_and_sd = function(x) {
    ##   
    ##   if (!is.numeric(x)) {
    ##     stop("The input x should be numeric")
    ##   }
    ##   
    ##   if (length(x) < 5) {
    ##     stop("Only compute mean and sd when the input has 5 or more numbers")
    ##   }
    ##   
    ##   mean_x = mean(x, na.rm = TRUE)
    ##   sd_x = sd(x, na.rm = TRUE)
    ##   
    ##   tibble(
    ##     mean = mean_x, 
    ##     sd = sd_x
    ##   )
    ##   
    ## }

This will import the function for use here.

``` r
source("source/mean_and_sd.R")
```

``` r
mean_and_sd(x_vec)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  10.5  3.32

## Make up data ..

Let’s *simulate* some data

``` r
sim_df = 
  tibble(
    x = rnorm(n = 30, mean = 3, sd = 2)
  )

sim_df |> 
  summarize(
    mu_hat = mean(x),
    sigma_hat = sd(x)
  )
```

    ## # A tibble: 1 × 2
    ##   mu_hat sigma_hat
    ##    <dbl>     <dbl>
    ## 1   3.74      1.76

Write a function to do simulations. The inputs are

- `n_subj` is number of subjects
- `mu` is the true mean
- `sigma` is the true sd

Function simulates data from a normal and computes sample mean and sd.

(We wrote this in a code chunk last time; now it’s being sourced.)

``` r
source("source/sim_mean_sd.R")
```

Let’s run this function.

``` r
sim_mean_sd(mu = 48, 50)
```

    ## # A tibble: 1 × 2
    ##   mu_hat sigma_hat
    ##    <dbl>     <dbl>
    ## 1   47.8      2.28

``` r
sim_mean_sd(n_subj = 30)
```

    ## # A tibble: 1 × 2
    ##   mu_hat sigma_hat
    ##    <dbl>     <dbl>
    ## 1   3.09      1.91

Import the LoTR data

``` r
fellowship_ring = 
  read_excel("data/LotR_Words.xlsx", range = "B3:D6") |> 
  mutate(movie = "Fellowship of the Ring")

two_towers = 
  read_excel("data/LotR_Words.xlsx", range = "F3:H6") |> 
  mutate(movie = "Two Towers")

return_of_the_king = 
  read_excel("data/LotR_Words.xlsx", range = "J3:L6") |> 
  mutate(movie = "Return of the King")

lotr_df = 
  bind_rows(fellowship_ring, two_towers, return_of_the_king)
```

Turn this into a function

``` r
lotr_import = function(cell_range, movie_title) {
  
  df = 
    read_excel("data/LotR_Words.xlsx", range = cell_range) |> 
    mutate(movie = movie_title)
  
  df
  
}

fellowship = lotr_import(cell_range = "B3:D6", movie_title = "Fellowship")
two_towers = lotr_import(cell_range = "F3:H6", movie_title = "Two Towers")
return =     lotr_import(cell_range = "J3:L6", movie_title = "Return")

bind_rows(fellowship, two_towers, return)
```

    ## # A tibble: 9 × 4
    ##   Race   Female  Male movie     
    ##   <chr>   <dbl> <dbl> <chr>     
    ## 1 Elf      1229   971 Fellowship
    ## 2 Hobbit     14  3644 Fellowship
    ## 3 Man         0  1995 Fellowship
    ## 4 Elf       331   513 Two Towers
    ## 5 Hobbit      0  2463 Two Towers
    ## 6 Man       401  3589 Two Towers
    ## 7 Elf       183   510 Return    
    ## 8 Hobbit      2  2673 Return    
    ## 9 Man       268  2459 Return

Look at one more example.

``` r
nsduh_url = "http://samhda.s3-us-gov-west-1.amazonaws.com/s3fs-public/field-uploads/2k15StateFiles/NSDUHsaeShortTermCHG2015.htm"

nsduh_html = read_html(nsduh_url)

data_marj_year = 
  nsduh_html |> 
  html_table() |> 
  nth(1) |>
  slice(-1) |> 
  select(-contains("P Value")) |>
  pivot_longer(
    -State,
    names_to = "age_year", 
    values_to = "percent") |>
  separate(age_year, into = c("age", "year"), sep = "\\(") |>
  mutate(
    year = str_replace(year, "\\)", ""),
    percent = str_replace(percent, "[a-c]$", ""),
    percent = as.numeric(percent)) |>
  filter(!(State %in% c("Total U.S.", "Northeast", "Midwest", "South", "West")))

data_marj_month = 
  nsduh_html |> 
  html_table() |> 
  nth(2) |>
  slice(-1) |> 
  select(-contains("P Value")) |>
  pivot_longer(
    -State,
    names_to = "age_year", 
    values_to = "percent") |>
  separate(age_year, into = c("age", "year"), sep = "\\(") |>
  mutate(
    year = str_replace(year, "\\)", ""),
    percent = str_replace(percent, "[a-c]$", ""),
    percent = as.numeric(percent)) |>
  filter(!(State %in% c("Total U.S.", "Northeast", "Midwest", "South", "West")))

data_marj_first = 
  nsduh_html |> 
  html_table() |> 
  nth(3) |>
  slice(-1) |> 
  select(-contains("P Value")) |>
  pivot_longer(
    -State,
    names_to = "age_year", 
    values_to = "percent") |>
  separate(age_year, into = c("age", "year"), sep = "\\(") |>
  mutate(
    year = str_replace(year, "\\)", ""),
    percent = str_replace(percent, "[a-c]$", ""),
    percent = as.numeric(percent)) |>
  filter(!(State %in% c("Total U.S.", "Northeast", "Midwest", "South", "West")))
```

write an import function

``` r
nsduh_import = function(html, table_num) {
  
  data = 
    html |> 
    html_table() |> 
    nth(table_num) |>
    slice(-1) |> 
    select(-contains("P Value")) |>
    pivot_longer(
      -State,
      names_to = "age_year", 
      values_to = "percent") |>
    separate(age_year, into = c("age", "year"), sep = "\\(") |>
    mutate(
      year = str_replace(year, "\\)", ""),
      percent = str_replace(percent, "[a-c]$", ""),
      percent = as.numeric(percent)) |>
    filter(!(State %in% c("Total U.S.", "Northeast", "Midwest", "South", "West")))
  
  data
  
}

nsduh_import(nsduh_html, table_num = 1)
```

    ## # A tibble: 510 × 4
    ##    State   age   year      percent
    ##    <chr>   <chr> <chr>       <dbl>
    ##  1 Alabama 12+   2013-2014    9.98
    ##  2 Alabama 12+   2014-2015    9.6 
    ##  3 Alabama 12-17 2013-2014    9.9 
    ##  4 Alabama 12-17 2014-2015    9.71
    ##  5 Alabama 18-25 2013-2014   27.0 
    ##  6 Alabama 18-25 2014-2015   26.1 
    ##  7 Alabama 26+   2013-2014    7.1 
    ##  8 Alabama 26+   2014-2015    6.81
    ##  9 Alabama 18+   2013-2014    9.99
    ## 10 Alabama 18+   2014-2015    9.59
    ## # ℹ 500 more rows

``` r
nsduh_import(nsduh_html, table_num = 2)
```

    ## # A tibble: 510 × 4
    ##    State   age   year      percent
    ##    <chr>   <chr> <chr>       <dbl>
    ##  1 Alabama 12+   2013-2014    5.57
    ##  2 Alabama 12+   2014-2015    5.35
    ##  3 Alabama 12-17 2013-2014    4.98
    ##  4 Alabama 12-17 2014-2015    5.16
    ##  5 Alabama 18-25 2013-2014   15.0 
    ##  6 Alabama 18-25 2014-2015   14.3 
    ##  7 Alabama 26+   2013-2014    4.03
    ##  8 Alabama 26+   2014-2015    3.86
    ##  9 Alabama 18+   2013-2014    5.63
    ## 10 Alabama 18+   2014-2015    5.37
    ## # ℹ 500 more rows

``` r
nsduh_import(nsduh_html, table_num = 3)
```

    ## # A tibble: 510 × 4
    ##    State   age   year      percent
    ##    <chr>   <chr> <chr>       <dbl>
    ##  1 Alabama 12+   2013-2014    1.42
    ##  2 Alabama 12+   2014-2015    1.49
    ##  3 Alabama 12-17 2013-2014    4.46
    ##  4 Alabama 12-17 2014-2015    4.36
    ##  5 Alabama 18-25 2013-2014    6.04
    ##  6 Alabama 18-25 2014-2015    6.39
    ##  7 Alabama 26+   2013-2014    0.15
    ##  8 Alabama 26+   2014-2015    0.2 
    ##  9 Alabama 18+   2013-2014    0.95
    ## 10 Alabama 18+   2014-2015    1.05
    ## # ℹ 500 more rows
